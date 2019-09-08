This is my first attempt at being focused with the way that I do my
programming. Here is how this is going to go.

Firstly, I am going to talk about some requirements of the project. Basically,
I want to get it layed out exactly what the program is supposed to do. In other
words, I want to create a reason why someone might want to use my program for
their purposes.

Next, I am going to tell a bit about some design decisions to be made. This
will extend pretty directly from the requirements, but this document will be
more structured in the sense that I will have some more explicit design
decisions embedded in the work.

After that I will actually get to the implementation of the thing. The first
goal will just be creating a bunch of files that should work on their own. I
don't want to be pre-alpha testing as much as I usually do. Or perhaps a better
way to put it is that I want to get a good pre-alpha testing process working so
that I won't have to do anything crazy to test a new module or function. If my
design is sound, I should be able to start at the bottom of my implementation
and test each individual module as I write it by simply opening up a python
interpreter and importing the thing that I am working on. This is still the
biggest kink in my process.

Lastly, I want to go through a polishing phase. This is basically like an alpha
testing phase, where I test some of the various things, try and break it like
an end user might, and make sure that all of the functionality of the
requiremntes document is there and that no extemeraneous functionality is
there, and if it is at least make sure that then extra stuff doesn't break the
thing. So that's that.

What does this mean for my MTG monte carlo box opening simulator?

Essentially it means that I need to stop writing in this document and go to my
requirements. But before I do that, I want to continue my freewriting for a bit
to see what the fuck this thing is.

So here is the problem. I am a classic Timmy when it comes to MTG stuff. I love
cards. I love the art. I love the design. I love the way they interact. I have
always loved card games ever since I was a kid.

Unfortunately for me, my father was raised in a family that demonized gambling.
As such, anything cards or card related (except for the standard 52 card deck
which my mother grew up playing with with my great grandfather) was strictly
looked at as "the spawn of the devil" and while we were allowed to use cards as
a child it was always thought upon as something that could only be given a very
short leash. At the slightest hint of discomfort or abrassion in the act of
buying and collecting these cards the plug would be pulled and restrictions
would be put in place to inhibit us from buying, playing, or otherwise
interacting with these cards ever again.

Well, now that I am an adult (HA!) I want to play MTG. I am a big boy now and I
get to do big boy things, and one of the big boy things is picking up a
children's card game and taking it way to seriously.

As a result of my repressed childhood (at least in terms of cards not
withstanding any other points about religion or open thought or anything else)
I have developed something of an addictive personality. This is great (or at
least, it's better than being depressed) but what it means is that I must be
careful with the things that I become enthusiastic about. Since my enthusiasum
for MTG has come along immediately following the loss of my previous position
at Alliant systems, this means that while I would love to throw all of my money
at Wizards of the Coast and justify it by saying that it is my money to do what
I want with and there is nothing anyone can tell me to convince me otherwise,
it is also the case that there are most certainly better ways for me to spend
my money and I need to convince myself to pursue those things rather than blow
off all my money on MTG boxes.

Which brings us to the motivation of this project. I want to run a simulator to
see what sorts of schematics and logistics need to be run on MTG boxes in order
to justify buying a box. In other words, while I already know that buying boxes
with the hopes of selling the singles is something that only Game Stores and
otherwise interested businesses should do to turn any kind of profit (because
selling cards will always happen at a loss unless you are the one that
specifically sets the price and you need to be a gamestore in order to set your
own price) I am not sure just how bad the ecosystem is for openning boxes, and
I would like to have some cold hard numbers to go by to help understand what is
the best way to see what actually happens monetary and probability wise when a
box gets cracked.

My vision for how this thing works is pretty simple. We start with some spread
to layout some statistics about cards. Something like the spread of rarity of
the cards, the spread of that rarity across print sheets, and then the spread
of those sheets into boxes. Obviously I don't know how WotC does their shit and
there is no way for me to know, but what I do know is that they have to have
some sort of schemanized process for doing what they do, and the people over
there can't be that much smarter than I am when it comes to putting together an
optimal spread of value. So while my system will not predict the market share
of cards by any means, it will at least aim to imitate Wizard's process so that
I can get a pretty good idea not about Wizard's process itself but instead
about how a process like this "could be" managed. So yeah.

The first thing to get done for this project will just be to get the model for
the stuff. A class like "MTGCard" or something similar is the most obvious way
to go, but from there I will need to assign print sheets to cards and sets to
printsheets. I also need to figure out a way to "construct" a box and once I am
able to do that, I need to figure out a way to open some boxes and then
evaluate critera for the completion of the overall process.

So that gives a pretty good starting point as far as where to begin with
requirements. I am getting to the rambly point of the freewriting which means I
need to go through something and figure out what I need to talk about.

On with the requirements!


