This [MQ2](https://www.macroquest2.com) macro is designed to assist you with your summonings and allow you to create a default summon set.
It was originally `SummonFD`, and it just focused on a couple of sections (Food and Drink).
However, I wanted it to work faster and I wanted three sections.
I made everything a bit more dynamic so that you can have as sections as you want with whatever name you want.
I mostly use it to summon [cookies](http://everquest.allakhazam.com/db/item.html?item=104648), [milk](http://everquest.allakhazam.com/db/item.html?item=90001), and [tea](http://everquest.allakhazam.com/db/item.html?item=113131) for my bot squad at the start of a session.

# Quick Implementation

![MQ2 Console Output](https://i.imgur.com/JwH6Axt.png)

## Quick Setup

- Put the `Summon.mac` file in your *Macros* folder.
- Run `/mac summon` from in game; this will create your initial `INI` file.
- Make adjustements as needed.
- Profit.

## Quick Usage

> /mac summon [stacks [food|drink]]

- stacks = # stacks to summon (default to whatever is set per section)
- no addtional parameters will summon whatever is defined in `Settings>DefaultSummon`, otherwise specify which one(s)

```
/mac summon           -> summons the quantities of each section defined in `Settings>DefaultSummon` in the INI.
/mac summon 3         -> summons 3 stacks of each section defined in `Settings>DefaultSummon` in the INI.
/mac summon 2 drink   -> summons 2 stacks of drink.
```

All of these commands includes checking inventory for any existing items.

# Detailed Usage

## Settings

- `LogDebug`: *Optional, Boolean; Default `FALSE`.* Will turn on debug logging to the MQ2 console; this is more detailed than *verbose*.
- `LogVerbose`: *Optional, Boolean; Default `FALSE`.* Will turn on verbose logging to the MQ2 console.
- `DefaultSummon`: *Optional, String; if not defined, cannot use `/mac summon`.* This defines which sections will be summoned by default. Multiple sections can be defined and should be separated by a pipe (`|`). The names of the other sections are up to you.

## Additional Sections

All of the additional sections are dynamically named; this means you can name them whatever you want.
I suggest sticking to single-word names to avoid bugs and ensure sanity.
Each section does have a few required and optional options as shown:

- `Name`: *Required, String.*
  - If a spell (gem), the name of the spell to memorize.
  - If an item, the name of the item to use.
  - If an AA, the name of the AA.
- `Cast`: *Required, String.*
  - If a spell, the gem number with the word gem: `gem8`.
  - If an item, the name of the item to use; yes, the same as the *Name* option.
  - If an AA, the aa number with the word aa: `aa12345`.
- `Item`: *Required, String.* The name of the item that is summon. This is used for inventory management.
- `Qty`: *Optional, Int; Default `1`.* The number of stacks of *Items* to summon. While this is normally stacks, it can be a quantity of each instead by using the *QtyIsByStack* option.
- `QtyIsByStack`: *Optional, Boolean; Default `TRUE`.* Decides if the *Qty* option is by stack or by each item.
- `QtyInStack`: *Optional, Int; Default `20`.* The number of *Items* in a stack. While everything I work with is 20 items per stack, things change and some items have larger stacks. So, I let you overwrite the default here.

# Example INI

```ini
[Settings]
LogDebug=TRUE
LogVerbose=TRUE
DefaultSummon=Food|Drink

[Food]
Name=Summon Food
Cast=gem4
Item=Summoned: Black Bread
Qty=1                            ; Optional, this shows you the default value
QtyIsByStack=TRUE                ; Optional, this shows you the default value
QtyInStack=20                    ; Optional, this shows you the default value

[Drink]
Name=Summon Drink
Cast=gem5
Item=Summoned: Globe of Water
Qty=1                            ; Optional, this shows you the default value
QtyIsByStack=TRUE                ; Optional, this shows you the default value
QtyInStack=20                    ; Optional, this shows you the default value

[Cookies]
Name=Fresh Cookie Dispenser
Cast=Fresh Cookie Dispenser
Item=Fresh Cookie
Qty=1                            ; Optional, this shows you the default value
QtyIsByStack=TRUE                ; Optional, this shows you the default value
QtyInStack=20                    ; Optional, this shows you the default value

[Milk]
Name=Warm Milk Dispenser
Cast=Warm Milk Dispenser
Item=Warm Milk
Qty=1                            ; Optional, this shows you the default value
QtyIsByStack=TRUE                ; Optional, this shows you the default value
QtyInStack=20                    ; Optional, this shows you the default value
```

# My Implementation

My actual INI file is here is provided in this repo: [Summon_Vert_RodcetNife.ini](https://github.com/VertigoRay/MQ2-Summon/blob/master/Summon_Vert_RodcetNife.ini).
Here's how I use it:

- When I login to the game and I want to solo, I type: `/mac summon 1 cookies|milk`
  - This overwrites the `Settings>DefaultSummon` option and just summons one stack of both the *Cookies* and *Milk* sections.
- When I login to the game and I want to bot with my ful group, I type: `/mac summon`
  - Since `Settings>DefaultSummon` is set to `Cookies|Milk|Tea`, my toon will summon the items and quantities defined in each of those sections:
    - [Cookies](http://everquest.allakhazam.com/db/item.html?item=104648): 6 stacks of 20, totaling 120 cookies.
    - [Milk](http://everquest.allakhazam.com/db/item.html?item=90001): 3 stacks of 20, totaling 60 glasses of milk.
    - [Tea](http://everquest.allakhazam.com/db/item.html?item=113131): 3 stacks of 20, totaling 60 glasses of tea.
    
![Summoning In Progress](https://i.imgur.com/s8u62hV.png)

# Notes

## Change Log

Revised and mostly re-written: 2019 Jul 27

- Improved to handle more than just two summon types.
- Sections are dynamically named by the user.

Originaly SummonFD, part of MMO Bug's download:

- hacked together from some unknown public authors by htw 12-03-18
- Was in a hurry and not thouroughly tested but it should get the job done!
