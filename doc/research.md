MTG Monte Carlo Simulator Research Findings
--------------------------------------------------------------------------------
Sources:
    [1] mtg.gamepedia.com/Print_sheet
    [2] https://boardgames.stackexchange.com/questions/19122/statistics-on-a-booster-pack-to-make-my-own-re-pack
    [3] https://magic.wizards.com/en/articles/archive/feature/building-tariel-2011-06-06

    {Ripped directly from [1]}
Nowadays, regular sized cards are printed on 11 x 11 sheets. Each regular
printing sheet features only cards of one rarity and language. The mythic rares
are included on the rare sheet. Extras like tokens and informational cards may
be used to fill in the empty spots. The cards are printed in a quantity
distribution of (1:7):24:88 (mythic:rare:uncommon:common). This is one rare (+
mythic) sheet for 3 uncommon sheets and 11 common sheets (10 if one land sheet
is used). The sheets are also printed in different quantities by language.

In the 16 card boosters of the latest sets, one is a marketing card, one is a
rare or mythic rare, three are from the uncommon sheet(s), 10 from the common
sheet(s) and one from the basic land sheet. For each 8 packs, the rare is a
mythic rare.


    {From a spreadsheet on [1]}
This code represents the number of times the card appears on the common print
sheet, making "C2" commons twice as abundant as "C1" commons.

2014-07 Magic 2015
    Total: 284
    MR: 15
    R: 53
    U: 80
    C: 101
    B: 20
    Other: 15
Sheet 1: 15 R1 53 R2
Sheet 2: 40 U3, 1 filler
Sheet 3: 40 U3, 1 filler
Sheet 4: 60 C2, 1 C1
Sheet 5: 40 C3, 1 C1
Sheet 6: 20 B6, 1 filler

Sheets 4 and 5 are printed in a ratio of 3:2

The C1 on both is the same card,
making it slightly more rare than the other commons.  The fifteen extra cards
(5R, 4U, 6C) only appear on the sheets for the sample decks.

    {Ripped directly from the top answer of [2]}
A normal Born of the Gods booster contains 10 commons, made up of 4–6 commons
from list A and 4–6 commons from list B. This means that certain combinations
of commons are likely to occur together, and other combinations of commons can
never occur together.

{ Based upon my research along with the fact that this project does not require
an exact level of precision when it comes to predicting magic card spreads (at
least not yet) I have decided to make the following assumption which is
probably incorrect but close enough to the truth for my purposes. This
assumption is that once the sheets are printed, the rare slot will come with
any one card from the rare sheet, the three uncommon slots will come randomly
from either of the uncommon sheets with no duplicates, and for the common
slots, four of the slots will be from sheet 4 with no dupes, and six of the
slots will come from sheet 5 with no dupes. While this is certainly not
correct, it is correct enough for my purposes }
