MTG Monte Carlo Simulator
--------------------------------------------------------------------------------
Design Document
================================================================================

    Throughout, the prefix MTG will be used as a placeholder for a keywords
    specific to this project.

A Model, View, Controller paradigm will be used for this project. A fourth
paradigm, the "MTGCore" compontents of project, will consist of universal
things, like the "Card class" (if specific cards need to be taken in to
account) or "Printsheet class" and so forth.

The controller will consist of a single file "MTGController.py" and will
contain a single class which is composed of many functions corresponding to
usecases from the requirements documents. The controller will have a member
which represents the model (call it MTGModel for simplicity). It will also
contain any other members needed to keep track of data (perhaps a robust
MTGData class in the future, but for now a simple list of what will be later
defined as an MTGSet) A single instance of this controller will be instansiated
by the "MTGView" upon begining of the program, and the view will call the
methods of this controller throughout its processes. The view will not have
access to the model methods but it will have access to all of the core
components. As such, the hierchy from the bottom up (and this project will be
designed bottom up) will look like this.

    Lowest Layer: MTGCore
        (Not one specific class but instead a collection of other MTG classes)
    Backend: MTGModel (Methods return MTGCore or otherwise "core-like" objects)
    Controller: MTGController (Methods represent use-cases of the project)
    View: MTGView (GUI magic takes place here, but for now it's simple text based)

The View will not have access to the Backend but will have access to
MTGController and to MTGCore.

The first layer of design to consider is the MTGCore classes, being the
bottom-most layer of this project. In sticking to the simple use case of
opening a booster box and examining the contents, the core will be something
like this...

Second from the top of this Four-tiered MTGCore layer is the MTGBoosterBox.
This class will be a simple list of MTGBoosterPack which is in reality just a
list of numbers (which we will call the "set number" of a card, represented as
e.g. 079/264 in the case of "Bolas Citadel" of the "War of the Spark" set). An
MTGPrintSheet is a bottom level concept containing a member that is a simple
dictionary from a two dimensional point to a number (the aforementioned "set
number"). Finally, an MTGSet will be the topmost concept. It will contain a
List of MTGPrintSheets and some member which represents metadata about how a
booster box is created. (Note here that we say simply metadata.  For now let us
say this is an enum, call it "MTGSetConstructionMethod" and it will have one
member which is "Standard15CardMethod" or something such ridiculous and that is
it. It is up to the job of the MTGModel to actually implement the construction
of a MTGBoosterBox from a MTGSet.)

So to sumarrize: MTGPrintSheet, MTGBoosterPack, MTGBoosterBox, and MTGSet are
the four classes which are the most essential to the logic of how this thing
should be built.

    MTGPrintSheet will have a member which is a mapping from a two-dimensional
    point to a set-number.

    MTGBoosterPack will be a simple list of some number of integers (fifteen
    count in cases of latest Wizards of the Coast MTG related products)
    representing the set-number.

    MTGBoosterBox will be a list of MTGBoosterPack.

    MTGSet will have a member which is first a List of MTGPrintSheet and then
    an enum (for now) representing how a box should be constructed.

We will speak now about the MTGModel. Since our first use case (openning a box)
is simple, let us not complicate ourselves with crazy fancys and instead return
to the requirements document to find our way forward.

The MTGModel will have a function which takes in a JSON (or some other kind of
data object if we don't use JSON) object and returns an MTGSet. It will also
have a function which takes in an MTGBoosterBox outputs to JSON.

To fill in the gaps of our complete loop, we need a function that takes a
MTGSet (and probably a random seed) and constructs a BoosterBox out of it, and
for the sake of our own sanity we should probably add a function that takes a
booster box and represents it as a dictionary from Integer to Integer (being
the aforementioned "Set-Number" to the number of cards acquired in that slot).

To summarize, the MTGModel will have the following methods:

    MTGModel:
        Set2BoosterBox  : MTGSet        -> MTGBoosterBox
        BoosterBox2Dict : MTGBoosterBox -> Dict<Int, Int>
        LoadMTGSet      : JSON          -> MTGSet
        WriteBoosterBox : MTGBoosterBox -> JSON

I am going to go with my initial instincts and say that these exact naming
schemes should be used. I will also go with my secondary instincts and say that
the MTGController, not the MTGModel, will keep the relevant persistant data.
After all, it is the job of the controller to maintain a database (or call a
database maintaining system) not the job of the MTGModel. Magic players don't
concern themselves with databases!

Now lets talk about the MTGController. I am done mincing words. This is what
the Controller Methods should look like.

    MTGController:
        1. LoadMTGSettings : Filename -> Void (MTGController initialized)
        2. GetMTGSets : Void (AfterINIT precondition) -> List of MTGSet
        3. SetOutputFile : String -> Void (Output file set)
        4. OpenBoosterBox : MTGSet -> Void (Output file written)

And the two most important members of MTGController:

    MTGController Members:
        - List of MTGSet
        - OutputFile : String
        - MTGState

MTGState is an enum which will be a private enum of the MTGController file. The
other members will probbaly be part of an "MTGData" class later but for now
this is fine.

Before we talk about the text-based MTGView, let us first go over the
generalized process that we know we must undergo. Firstly (as the program
begins) whatever "booter" class is used (which contains the "main" method)
should create an MTGView instance and call the "Boot" function or whatever of
that MTGView object.

Next, the boot method of the MTGView should initialize an MTGController.
First the booter will discover a settings file. Second it will feed that file
(with hopefully well formed JSON) to the Controller so that the controller may
initialize itself.

Once the controller is ready, the booter should pass control to the primary
loop. The Primary loop will prompt the user for a number (after printing the
options to the user on the screen) when the user enters the number, the
hardcoded function developed in to that number will be called. For example, if
the prompt looks something like ...

    0. Exit
    1. Clear Settings
    2. Add Settings
    3. Show Sets
    4. Set Output Location
    5. Open Booster Box
    > _

The user could input 2 (which will prompt them for a filename) and then input
their filename, which the program will then read and process and pass control
back to the user with feedback on what went down after it loads the stuff in.

If the user enters anything but a number at this point, the program should
chastise them and display the prompts again.

Suppose the user wants to open a booster box. From program start, the literal
user input might look something like this, (with the thoughts of the user in
parens)

    3 (Hm, no sets loaded, I should probably use option 2 to add settings)
    2 (Okay it's prompting for an input file. Let's use the prebuilt JSON)
    prebuilt.json (Nice, I got feedback that told me its loaded. Lets make sure)
    3 (Nice! It shows 0 -> Thrones of Eldraine as a set now. Let's config the output now.)
    4 ELD (Good, feedback that all box openings will be saved to this file)
    5 (Nice, it says ELD001.box was written, lets check it out)
    Windows Explorer -> Navigate to working directory -> Open ELD001.box with vim
    (Sweet! A nice ASCII representation of the box opening is here. This program is cool!)
    5 (And ELD002.box is written)
    Open ELD002.box with vim (Nice, the entire thing has a complete usage cycle!)
    (This developer makes me feel sexually aroused right now)

(Please spare this lonesome developer the joys of thinking that his clients get
as much sexual satisfaction out of using a good program as he does.)

I believe this process has been more constructive than detailing out the exact
methods of the view. I mostly just wanted to show a super oldschool method of
interfacing with the user. I hate frontend programing, so this is how I like to
do things. It's not very pretty but it's super clear and it makes my mind
happy.

So yeah, that about covers it.

