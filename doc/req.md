MTG Monte Carlo Simulator
--------------------------------------------------------------------------------
Requirements Document
================================================================================

The MTG Monte Carlo Simulator is a command line program. When it begins it will
receive input from a settings file. This settings file will at least contain
information about the critical information about the set of cards which is to
be evaluated. For the initial iteration of the simulator, this information is
the following.

    1. A map from each location on the printsheets to a number.
    2. Metadata indicating the method of construction of a booster pack.
    3. The number of booster packs in a box.

The simulator shall prompt the user for a use case. The first use case to be
implemented will be a simple box opening. The results of this box opening will
be saved to an output file. Once this use case is operational, an extension to
allow the user to choose the number of boxes will be added straightforwardly.

The next use case to be implemented will be an inquiry in to the number of
boxes opened to meet a certain "collection requirement". That is, if the user
would like to know how many boxes they need to open (as a gambler, not a
statistician) to get a full playset of the commons, they will be able to run
this use case. Similarly, once this is in place, this process can be put on a
loop to determine a statistical average.
