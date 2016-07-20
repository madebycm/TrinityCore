*The Big Book of Bots.....*   
*The Mega Manual of Minions....*   
*blah..*   
# [ THE BOTS GUIDE ]
>Compiled by: Thesawolf (@ Gmail dot Com)   
>Version 0.3 - 20 July 2016

---------------------------------------
### Sections (clickable links to jump to each section)
1. [Introduction](#introduction)
    - [Extended Credits](#extended-credits)
    - [Donations](#donations)
2. [NPCBots](#npcbots)
    - [NPCBot Commands](#npcbot-commands)
    - [NPCBot Control and Usage](#npcbot-control-and-usage)
        - [NPCBot Getting Started](#npcbot-getting-started)
        - [NPCBot Getting Around](#npcbot-getting-around)
        - [NPCBot Equipment](#npcbot-equipment)
        - [NPCBot Roles](#npcbot-roles)
        - [NPCBot Formation](#npcbot-formation)
        - [NPCBot Abilities](#npcbot-abilities)
        - [NPCBot Grouping](#npcbot-grouping)
        - [NPCBot Extras](#npcbot-extras)
    - [NPCBot Config Settings](#npcbot-config-settings)
    - [NPCBot Database Information](#npcbot-database-information)
    - [NPCBot System Usage Information](#npcbot-system-usage-information)
3. [PlayerBots](#playerbots)
    - [PlayerBot Commands](#playerbot-commands)
    - [PlayerBot Control and Usage](#playerbot-control-and-usage)
        - [PlayerBot Getting Started](#playerbot-getting-started)
        - [PlayerBot Getting Around](#playerbot-getting-around)
        - [PlayerBot Equipment](#playerbot-equipment)
        - [PlayerBot Roles](#playerbot-roles)
        - [PlayerBot Formation](#playerbot-formation)
        - [PlayerBot Abilities](#playerbot-abilities)
        - [PlayerBot Grouping](#playerbot-grouping)
        - [PlayerBot Extras](#playerbot-extras)
    - [PlayerBot Config Settings](#playerbot-config-settings)
    - [PlayerBot Database Information](#playerbot-database-information)
    - [PlayerBot System Usage Information](#playerbot-system-usage-information)
4. [Thesawolf Enhancements](#thesawolf-enhancements)
5. [Guide Changelog](#guide-changelog)

---------------------------------------
## Introduction
First and foremost, please be aware that I do NOT take credit for the the coding, development and
documentation for all the marvels of engineering found in the "NPCBots" nor the "PlayerBots", that distinction
goes toward the known authors of those respective bot systems listed below:

- PlayerBots (aka MaNGOS-Bots) by ike3 (https://github.com/ike3/mangosbot)  
	Originally developed by Blueboy (https://github.com/playerbot/mangos)  
	with various enhancements by Thesawolf (hey, that's me) (https://github.com/thesawolf/TrinityCore)
- NPCBots (aka NewNPCBots, LordPsyanBots, MinionBots) by LordPsyan (https://bitbucket.org/lordpsyan/lordpsyan-patches)  
	with numerous enhancements by Graff/Trickerer (https://bitbucket.org/trickerer/trinity-bots/src)  
	and various enhancements by Thesawolf (hey, that's me again.. repo the same as previous)

This guide is an ATTEMPT to better, and fully, document the commands and usage examples for the respective
bot systems.   
Please note that while every attempt is made to do so, this guide may not (nor ever) be 100% complete or thorough (but I'll try).

### Extended Credits
Beyond the original authors, I wanted to setup a little thanks area for those that helped contribute to my coding efforts (either through data
submissions, great ideas/feedback or even donations). Yes, I'm putting this near the front because these folks obviously deserve to have their names
acknowledged before you get into the nitty-gritty of the Bots.

- [Conan513](http://www.ac-web.org/forums/member.php?234688-conan513gm)
Thanking Conan for his excellent work on SPP and inclusion of alot of my work in
it. As well as all the awesome feedback and thoughts about features/fixes.
- [dmanbob](http://www.ac-web.org/forums/member.php?208219-dmanbob)
Thanks to dmanbob for assistance with data needed for working on NPCBot
lookup. His legwork saved me alot of time and frustration. Also, thanks for
some of his feedback and some of his features/scripts I've used in the past
(NPCs with smart scripts)

### Donations
Some folks mentioned putting up a donation link so I figured I'd put one up
in here just in case anyone wanted to actually use it and so that no one
confused where donations should go if I put the link up in someone's project
thread (if you are going to donate, you should always donate to a project
owner first.. they are the one that brings these to the masses, I just code in the
background and don't want to detract from the awesome work on someone's
repack)

:+1: [PayPal Donation](https://www.paypal.com/cgi-bin/webscr?cmd=_s-xclick&hosted_button_id=3DXNFF3T34HSS)

---------------------------------------
## NPCBOTS
NPCBots are minion-like bots that have limited functionality and control. They follow you around, buff you, attack things and occassionally they can do class-specific things like summon drink/water, open portals, summon healthstones, etc. They are most handy at lower levels or outside dungeons/raids although they CAN do dungeons and raids, but expect some frustrations due to the lack of controls for them.

Some features of the NPCBots:
- Grouping
- Buffing
- Fighting (via spells, melee, ranged combat)
- Healing
- Resurrecting
- DungeonFinder (they can enter dungeons with you)
- Raids (they can participate in raids)
- PvP (they can fight members of your opposing faction)
- Summon Food/Drink (mages)
- Summon Healthstones, Soulstones (warlocks)
- Emote responsiveness (will respond in various ways to any emote)
- Riding mounts
- Be placed in locations (for future hiring, or as a buff station, etc.)
- Change their gear
- Change their roles
- etc...

### NPCBot Commands
Command references are current up to the date of this documentation (and includes the various enhancements) by myself and may not be applicable to all installations out there. If a command doesn't show up in the listing or gives an error message that it's invalid.. there's a good chance that install/repack doesn't have a "current" codebase.

Also, please note that command access is dependent upon the installation you are using and some commands may not be
available to all accounts (depending on their access level and permissions set in the RBAC tables). Optionally, you can make RBAC adjustments by yourself with tools such as phpmyadmin, HeidiSQL to the rbac tables in the 'auth' database, but that is beyond the scope of this document.
```
KEY:
< > (less/greater than) indicates infon or action you need for the command, can be left out to list info
 |  (pipe character) indicates parameter options (i.e. this|that  = this OR that)
 -- (two dashes) indicates information follows about the command
```
**COMMAND**: **`.npcbot`** (by itself will list all syntax available)
- **`lookup <CLASS>`** -- lookup the available npcbot Name/ID by class#
    - _CLASS_ = Class# of npcbots (i.e. 1 for WARRIORs)   
    **Example Usage**:
        - `.npcbot lookup` (to list all classes)
        - `.npcbot lookup 1` (to list all Warriors)
- **`add <ENTRY>`** -- adds npcbot bypassing the price conditions
	- _ENTRY_ = ID# of npcbot (obtained from lookup list)   
	**Example Usage**:
	    - `.npcbot add 70001` (to add npcbot with ID 70001 from lookup list)
- **`spawn <ENTRY>`** -- adds npcbot
    - _ENTRY_ = ID# of npcbot (obtained from lookup list)   
	**Example Usage**:
        - `.npcbot spawn 70001` (to spawn npcbot with ID 70001 from lookup list)
- **`set <faction|owner> TARGET`**
    - `faction <a|h|m|f> TARGET` -- sets the selected npcbot faction manually
        - _a_ = alliance
		- _h_ = horde
		- _m_ = monster
		- _f_ = friendly to all
		- _TARGET_ = selected NPCBot
	- `owner <GUID|NAME> TARGET` -- sets ownership of a selected npcbot to a specific player
		- _GUID_ = guID of a player (in database)
		- _NAME_ = name of a player
		- _TARGET_ = selected npcbot   
        **Example Usage:**
            - `.npcbot set` (displays list of subcommands)
			- `.npcbot set faction` (displays list of subcommands for faction)
			- `.npcbot set faction a TARGET` (sets the selected NPCBot to Alliance)
			- `.npcbot set owner` (displays subcommand list)
			- `.npcbot set owner MyPlayer TARGET` (sets the selected NPCbot owner to MyPlayer)
- **`remove TARGET`** -- frees npcbot from control.
    (_NOTE_: If an npcbot is selected, this will remove that specific npcbot or if a PLAYER is selected, this will remove ALL npcbots they own.
The npcbot will then return to their spawned location.)
	- _TARGET_ = selected npcbot OR npcbots OF selected player, _see note above_   
	    **Example Usage:**
        - `.npcbot remove TARGET` (removes the selected npcbot or npcbots of selected player)
- **`delete TARGET`** -- deletes npcbot from control and active npcbot listing in database
	- _TARGET_ = selected npcbot OR npcbots OF selected player   
	    **Example Usage:**
        - `.npcbot delete TARGET` (deletes the selected npcbot or npcbots of selected player)
- **`revive TARGET`** -- revives selected npcbot. If player is selected, revives all npcbots of selected player)
	- _TARGET_ = selected npcbot OR npcbots OF selected player   
		**Example Usage:**
        - `.npcbot revive TARGET` (revives dead, selected npcbot or npcbots of selected player)
- **`cast`** -- dev only command and mostly deactivated code-wise
- **`info TARGET`** -- list npcbots' information for selected player or self
- **`reset TARGET`** -- resets selected npcbot. (_NOTE_: Cannot be used in combat)
- **`command <COMMAND>`** -- forces ALL npcbot followers to either FOLLOW or STAY
	- `command <s|st|stay|stand|f|fo|fol|follow>` -- sets the npcbot stances manually
		- _s, st, stay, stand_ = STAY mode
		- _f, fo, fol, follow_ = FOLLOW mode   
            **Example Usage:**
            - `.npcbot command stay` (selected npcbot will stay at location)
	        - `.npcbot command follow` (selected npcbot will follow owner)
- **`distance <#>`**  -- sets ALL npcbots follow distance from owner
    (*NOTE*: If set to **0**, npcbots will follow passively (not attacking anything) until owner attacks something)
	- _#_ = value between 0 and 75 (75 being furthest distance away)   
		**Example Usage:**
        - `.npcbot distance 0` (selected npcbot will follow and not attack anything)
        - `.npcbot distance 75` (selected npcbot will follow you from furthest distance)

### NPCBot Control and Usage
#### NPCBot Getting started
If this is your first time using an NPCBot, you'll need to do the following to get started:
- `.npcbot lookup`
    This will give you a listing of the available classes with an ID to indicate each class. For example, 1 could be the Class ID for Warriors.   
    _Example Output_:
```
.npcbot lookup #class
Looks up npcbots by #class, and return all matches with their creature ID's.
BOT_CLASS_WARRIOR = 1
BOT_CLASS_PALADIN = 2
BOT_CLASS_HUNTER = 3
BOT_CLASS_ROGUE = 4
BOT_CLASS_PRIEST = 5
BOT_CLASS_DEATH_KNIGHT = 6
BOT_CLASS_SHAMAN = 7
BOT_CLASS_MAGE = 8
BOT_CLASS_WARLOCK = 9
BOT_CLASS_DRUID = 11
BOT_CLASS_BM = 12
```

After you have figured out which class you want to lookup NPCBots in:
- `.npcbot lookup 1`
    For this example, we'll look for Warrior NPCBots.   
    _Example Output_:
```
Looking for bots of class 1...
70146 - [Wu]
70147 - [Ilsa]
70173 - [Darnath]
70175 - [Evencane]
70201 - [Kore]
70217 - [Ahonan]
70220 - [Behomat]
70224 - [Ruada]
```
Next, you'll select an NPCBot from the list:
- `.npcbot spawn 70224`
    For this example, we'll select _Ruada_ with an ID of 70224

Ruada will spawn at your location as a level 80 Warrior (by default, NPCBots spawn as Level 80)
In previous versions of the NPCBots, they would spawn as Level 80 Monsters and would require you to manually set their faction. Now, NPCBot '_Thesawolf_' enhancements have NPCBots automatically spawning as the faction of the individual spawning them. In the event of some SetFaction failure, the NPCBot will spawn with the "Friendly to All" faction so that they are not KoS (killed on sight) by city guards, etc. (another '_Thesawolf_' enhancement).   

Right-clicking on the NPCBot will open what's called a _Gossip Menu_ (which gives you some command choices)   
_Example Output_:
```
You need something?
- Will you follow me? (hire)
- Pick a side! (set faction)
- You can go now... (delete)
- Nevermind
```
Next, you'll most likely just select '_Will you follow me? (hire)_' which will popup a Hire box asking:   
"Do you wish to hire Ruada?", with a cost amount that you can _Accept_ or _Cancel_.

**REFERENCE**: The other options in the pre-hire Gossip include:
- _Will You follow me? (hire)_ - already discussed
- _Pick a side! (set faction)_ - this selection will open a submenu displaying:

```
- Alliance
- Horde
- Monster
- Friend to all
- (BACK)
```
This option will let you set an NPCBot's faction that will allow you to attack them as a Monster or as an opposing faction member for PvP, etc.
- _You can go now... (delete)_ - this selection will delete the NPCBot (in case you change your mind or need to cleanup NPCBots left in various areas)
- _Nevermind_ - this selection closes the pre-hire Gossip Menu

After hiring the NPCBot, they will automatically level themselves to your level (shouting "DING!" in the process).
Right-clicking on the NPCBot will open a new _Gossip Menu_ with an assortment of options (discussed in following subsections). Your NPCBot will follow you around in or out of group, but it's probably a good idea to get them into your group so you can monitor their location on mini-map, or health/mana, etc. Your new hired Gossip Menu will show:
```
- Manage equipment...
- Manage roles...
- Manage formation...
- Use ability...
- <Create Group>
- [OPTIONAL options may be displayed here]
- You are dismissed
- You are free to go (reset owner)
- You are fired! (remove)
- Nevermind
```

For now, select ___Create Group___ and your NPCBot will join your group and you can begin your adventures!
As mentioned previously, the other options will be discussed further down this document.

#### NPCBot Getting Around

Whether grouped or not, your NPCBot will follow you around, keeping you buffed along the way (if they can buff), healing you when needed (if it is a healer-type NPCBot), attacking things alongside you and even ressurecting you if you die (if they can ressurect, that is). NPCBots are designed to keep up to your run pace and will mount up on their own version of your mount when you do. In the event that they cannot keep up (due to you moving too fast or they being stuck in combat or in something), your NPCBot will eventually teleport to your location (even if you go into another zone). NOTE: NPCBots cannot teleport to you when you are in a dungeon, if they are not part of your group.

For the most part, go somewhere and they will follow. Simple as that.
In those cases where following might not be safe or you want to proceed safely, you have a few options.

**REFERENCE**: If your NPCBot is in your direct vicinity, you can target them and emote:
- `/wait` to make your NPCBot stay put
- `/followme` or `/beckon` to make your NPCBot follow you again

**REFERENCE**: If your NPCBot is not targetable or in the immediate vicinity (for selection), you can use the commands:
-  `.npcbot command stay` to make all your controlled NPCBots STAY
- `.npcbot command follow` to make all your controlled NPCBots FOLLOW

In the event your NPCBot is too far away to path to you, your NPCBot will teleport themself to you.

**REFERENCE**: Normally, when something attacks you, your NPCBot will come to your rescue and attack it with melee, spells or ranged skills. However, there may be times you are navigating tight areas and you don't want your NPCBot running off to your rescue. In those situations you can set your NPCBot to a "passive" mode by changing their distance. You can do this both in their Gossip Menu with the ___Manage Formation...___ selection and setting the distance to **0** or by using:
- `.npcbot distance 0` to make your NPCbot follow you closely and passively


___What happens to your NPCBot when you are not around?___ Don't worry... your NPCBot isn't hanging around outside the dungeon you decided to log out at. Unless, of course you spawned that NPCBot outside that dungeon. When you logout (or if your NPCBot is removed from control by other options), your NPCBot will return to their spawned location. If you picked up your NPCBot in Darnassus, it will return there. If you spawned your NPCBot on the road through the Barrens, it will return there. This can be both annoying and good, spawning NPCBots in a good central location (like in cities), will provide you an easy way to hire them (and coincidentally, they like to hang out and buff passerbys). However, spawning your NPCBot out in the middle of nowhere makes them rather inaccesible for rehire by other people (were you to release control). In situations like that, it is better to fire them (or delete them), so that they return to the spawnable NPCBot pool.

#### NPCBot Equipment

NPCBots give you the ability to customize their individual gear pieces to make them more effective in combat. (NOTE: Changing their gear does NOT change their appearance, as the NPCBots utilize NPC models rather than individual gear piece models like Players do. The exception to this are weapons.)

To upgrade/equip gear, you need to right-click that NPCBot and choose _Manage equipment..._ from their post-hire Gossip menu. You should then see the following:
```
- Show me your inventory
- Auto-equip...
- Main hand...
- Ranged...
- Head...
- Shoulders...
- Chest...
- Waist...
- Legs...
- Feet...
- Wrist...
- Hands...
- Back...
- Shirt...
- Finger 1...
- Finger 2...
- Trinket 1...
- Trinket 2...
- Neck...
- Unequip all
- BACK
```
As you can see, you can gear up pretty much every slot on your NPCBot (just remember that you will only see a visual change for weapon slot items)
- `Show me your inventory` will make the NPCBot whisper you a list of everything they currently have on with a designation of which piece of gear is in which slot
- `Auto-equip` will list out all the items you have in YOUR bags that the NPCBot can use. Clicking on one of those items will automatically give it to the NPCBot and equip it into the appropriate slot
- _(INDIVIDUAL GEAR SLOTS)_ will show you what they have equipped (if any), an option to use their old equipment (if any to start with) OR an unequip option (if you gave them some gear), a listing of any item in YOUR bags that the NPCBot can use in that slot and a BACK option. Selecting any of your bag items will automatically send that item to the NPCBot and have them equip it. The option to use old equipment or unequip gear will have the NPCBot RETURN the gear you gave them BACK to YOUR bags. They will then return to the default gear/state for that slot.
- `Unequip all` will have them do just that.. unequip all gear you have given them and return them to YOUR bags. (NOTE: When firing an NPCBot, any gear you have given your NPCBot will automatically be returned to you)
- `BACK` just goes back to the previous menu

#### NPCBot Roles

NPCBot Role management allows you to adjust how they operate overall. The available options are dependent upon the class of the NPCBot you are controlling. 

To adjust the NPCBot's roles, you need to right-click that NPCBot and choose _Manage roles..._ from their post-hire Gossip menu. You should then see (dependent upon the class):
```
- Tanking
- DPS
- Heal
- Ranged
- BACK
```
ACTIVE Roles will be noted with an icon depicting two crossed swords while INACTIVE Roles will be noted wih a chat bubble with dots inside (...)
Clicking on the respective Role will toggle it on/off (changing the icon).

The roles are just as they state. If you want your NPCBot to make more of a tanking (melee) role, select "_Tanking_". More DPS? Select "_DPS_". So on and so forth. Please be aware that selecting the "_Ranged_" role will result in the NPCBot ALWAYS trying to keep their distance from the mobs. If you are in tight quarters, setting to Ranged could result in the NPCBot leaving that tight area to stay away from the mob (which could easily result in pulling additional mobs). The "_BACK_" option returns to the previous menu, of course.

NPCBot Roles are pretty straight foreword and it's recommended to only enable 1 or 2 specific roles for that class to minimize them switching tactics around alot. 

#### NPCBot Formation
Some times you just want your NPCBot close.. or far away as possible. The formation option allows you to adjust your NPCBot's distance from you.

Select _Manage formation..._ from their post-hire Gossip menu to adjust the distance. You will see:
```
- Set distance (current: XX)
- BACK
```
Selecting "_Set distance_" will open up a popup window that you can enter in an amount. This amount can be anywhere from **0** to **75**. Setting any higher than 75 will default to 75 and any lower than 0 to 0. As mentioned previously, setting the distance to 0 will result in the NPCBot PASSIVELY following you rather closely and not engaging mobs unless you attack. 

#### NPCBot Abilities
NPCBots include a healthy sampling of real spells for each of the respective classes (NOTE: Not ALL class spells are represented or used). Some spells/abilities such as buffs, heals, remove curse/poison, etc. are available through an NPCBot's Ability menu. Additionally, some spells/abilities are only available when an NPCBot is at/over a certain level (much like real player restrictions)

Selecting _Use ability..._ from the Gossip menu will give you a listing of the available spells/abilities that they can cast on you or for you. The "Update" option will refresh the spell listing and the "BACK" option works the same as all the other Back options.

Not listed in the abilities is all the current spells/abilities that NPCBots use in COMBAT. These are usual class specific spells like Moonfire for Druids, etc. etc. Also, please note that the NPCBots are coded to use things like Root (Druids), Polymorph (Mages), Traps (Hunters), etc. for situations where CC (Crowd control) is needed. 

#### NPCBot Grouping
Although NPCBots will follow their owner around grouped or ungrouped and will usually buff people outside their groups, selecting the ___Create Group___ option will have them join your group and properly utilize group buffs for everyone in the group.

Grouping is required to properly utilize the DungeonFinder (as you cannot summon NPCBots in or into instances that are ungrouped)

>**NOTES**: There is a known issue where if you are in a group and get disconnected or kicked that the NPCBot(s) will remain in a group with their owner (thus showing up in both groups). The main group needs to kick the NPCBots from the group to be able to invite the owner of the NPCBots. This is the only workaround for that issue, at the moment.

>Because NPCBots are not considered real players, a dungeonfinder group's loot rules will be set to _Free For All_ rather than the _Group Loot_ usually auto-selected for pre-made groups. 

>Also, it is advised to fire any additional NPCBots that you might own outside of the group as there have been reports of issues with some quest completions and Random dungeon daily rewards when NPCBots are active but not a part of a group.

#### NPCBot Extras
Depending upon the class of the NPCBot, there may be extra options found in the Gossip menu for that NPCBot.

Most notably, Mage NPCBots will present the options:
```
- I need food
- I need drink
- Can we get a refreshment table?
- Can we get a portal?
```
These options will summon a stack of food or drink for you.
If your level is high enough, the mage NPCBot can summon a refreshment table.
Mage NPCBots can now summon portals (faction and level restrictions are
applied, meaning your mage will not summon a portal to the opposite faction
and will only summon portals that they would normally be able to summon at
that level (no low level Shattrath portal)

Additionally, Warlock NPCBots will present the options:
```
- I need a healthstone
- I need a firestone
- Can we get a soulwell?
```
These options will summon a healthstone or firestone for you.
If your level is high enough, the warlock NPCBot can summon a soulwell.
(Level restrictions are applied here, too)

Lastly, all NPCBots will have the following extra options:
```
- You are dismissed
- You are free to go (reset owner)
- You are fired! (remove)
- Nevermind
```
- `You are dismissed` will send the NPCBot back to their spawn location for the remainder of your gaming session
- `You are free to go` will reset the owner (thereby removing you as the owner) and send the NPCBot back to their spawn location. This is handy to allow other people to hire that NPCBot. There is an additional side effect that since the NPCBot still stays in the world, they will retain any gear given to them making them upgraded and available to all for hire.
- `You are fired` will delete the NPCBot from ownership and the game world and return them to the NPCBot pool for spawning. Deleting an NPCBot will make them return all gear you may have given them.
- `Nevermind` will simply close out the Gossip menu

### NPCBot Config Settings
(TODO: discuss the available config settings here)

### NPCBot Database information
NPCBot data is stored in the following locations:
- `characters` Database
    - `characters_npcbot` (this contains currently loaded npcbots)
	also uses:
	    - `character_inventory`
	    - `item_instance` (both for holding information about currently equipped gear for active npcbots)
- `world` Database (stores information in the following tables)
    - `creature_template` (ids 70001-71000)
    - `creature_template_outfits` (ids 70001-71000)
    - `creature_equip_template` (ids 70001-71000)
    - `creature_template_outfits` (ids 70001-71000)
    - `creature` (ids 70001-71000)
    - `npc_text` (ids 70001-71000)

If you wanted to make changes to the static template data used for NPCBots, you make adjustments
in the `world` Database to those specific ids in the above tables (i.e. npcbot model, outfits, etc.)

Live NPCBots (currently spawned into the world) are found in the `characters` Database

### NPCBot System Usage information
Bots are counted as active objects (keep grids loaded like players).  
Bots are being added to world at server loading (along with grids).  
If 2 or more bots are located in same grid, only one grid is loaded.  
If bot leaves grid where he was spawned (following player), that grid can be unloaded.  
Grid size is 533.333 (yd).  
Each grid loaded uses 30-50 Mb of memory.  
Each bot loaded (without grid) uses less than 0.2 Mb of memory.  
Current maximum bots to spawn: 245 (creature_template bot entries amount).  

---------------------------------------
## PLAYERBOTS

### PlayerBot Commands
#### PlayerBot Getting Started

#### PlayerBot Getting Around

#### PlayerBot Equipment

#### PlayerBot Roles

#### PlayerBot Formation

#### PlayerBot Abilities

#### PlayerBot Grouping

#### PlayerBot Extras

### PlayerBot Control and Usage

### PlayerBot Database Information

### PlayerBot System Usage Information

---------------------------------------
## Thesawolf Enhancements
Just providing this as reference to _some_ of the enhancements I've done to the NPCBot and PlayerBot codebases (doesn't neccessarily include references to all fixes I've done). Basicly, if you aren't seeing some of these functions in your repack, it's because your repack isn't using my current code commits. Please don't contact ME about it, contact your repack author to merge it in from my repo at: https://github.com/thesawolf/TrinityCore from my _TrinityCoreLegacy_ branch (but that's ultimately up to them). If you are a repack author or working on your own installation, please consider at least mentioning me in your credits or dropping me a line and saying thanks for the code features.

### NPCBot Enhancements: (in no particular order)
- Auto-set faction to owner faction at summoning (no more need to .npcbot set faction X)
- Addition of "friend to all" faction options/fallback
- Removed the NPCBot randomly attacking you after dismissing (yes, this was an actual coded in "feature" by the author)
- Expanded pre-hire Gossip menu to include deleting and setting faction
- Fixed NPCBots teleporting to master (segfault due to recent TC changes)
- Fixed NPCBot mounting speed (due to recent TC changes)
- Added in NPCBot responsiveness to 200+ emotes (they will usually say something witty and have an emote response of their own)
- /wait emote response triggers NPCBot staying
- /followme and /beckon emote response triggers NPCbot following
- Updated dormant NPCbot commands to allow .npcbot info, reset, distance X, and command stay/follow
- Expanded post-hire Gossip menu to include dismissing, reset owner, and firing (deleting)
- Fixed mage water/drink summoning
- Added mage refreshment table summoning
- Added warlock healthstone/firestones/soulwell summoning

### PlayerBot Enhancements: (in no particular order)
- Added in-depth .bot lookup feature (with graphical icons) to look for available bots (and alts)
- Auto-set faction, auto-init, auto-summon upon adding
- Fixed it so that the autosets weren't applying to alts summoned as playerbots
- Added NotSoRandom toggle to allow for preset bots (with random fallback rather than full-blown random chargen)
- Added ARAC (Any Race, Any Class) support toggle in the chargen process (still requires client ARAC support, tho)
- Fixed .bot command segfault
- Opened up a number of Playerbot commands to regular user level (rather than GM only)
- Implemented some level checking so that playerbots don't re-init all the time when added (default within 3 levels range)
- Added gearlock support toggle so that gearsets stay persistent through init/update/randoms (for those that like to dress their bots)

---------------------------------------
## Guide Changelog
Development tends to change alot (and hopefully this guide will reflect that). This Changelog should help to see what might've hapened to a feature you THOUGHT was available or if a feature gets deprecated, you can get a timeline when it happened.
- **Version 0.3** (_20 July 2016_)   
    - Jump to 0.3 since I added a bunch of information and didn't changelog
      them properly (oops)   
    - Added in and to the list of enhancements I'd coded for the Bots   
    - Added info about the NPCBot Mage and Warlock extra Gossip functions   
    - Added in section for NPCBot config file settings   
    - Added in extended credits for those that helped along the way
    - Added in a PayPal donation link (just in case and to keep it separate   
      from any projects using some of my fixes/features)   
- **Version 0.1** (_13 July 2016_)
    - NPCBot Information initial submit
        - added new info, reset, command, distance commands too

---------------------------------------
