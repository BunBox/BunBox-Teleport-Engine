# BunBox Teleport Engine
## Introduction

Thank you for your interest in the BunBox Teleport Engine.

This site serves as documentation for the Engine, providing explanation of core features, useage in greater detail and example use cases.

## How does this work?

### Summary
The Teleport Engine attachment is worn much like an AO is. Attached and forgotten about, allowed to do it's own thing.  
Once attached, scripted objects can trigger teleports by generating datapackets containing the data needed for the Engine to perform the teleport and then sending them to the user to be teleported via llRegionSayTo.

### Security in the Datapacket
This datapacket is accompanied by several layers of unique encrypted time-sensitive authentication data which is checked by the Engine for validity.  
These validity checks are per user, per teleport, per object and each teleport call must have its own unique datapacket with for loops being used for multiple teleports when a single event should trigger multiple TPs.

### Contents of the Datapacket
After these checks are made, the engine processes the datapacket to prepare the parameters of the teleport. 
These parameters include:
-	**Encrypted Sound UUID** - _A datapacket can contain the UUID of a sound to be played upon teleport by the Engine. This UUID is communicated in an encrypted format so to protect content creators, though it should be noticed UUIDs are things a malicious viewer can grab, but thats no reason to not do what we can._

-	**Teleport Data** - _Destination sim name, destination global position, destination local position OR destination offset._

-	**Anti-Abuse Flags** - _Scripts that communicate with the Engines directly instead of through the API are subject to serveral active checks to determine if the script is held inside an object that may be being used for malicious purposes. In the pre-made teleporter script included with the boxed Engine, this flag is tripped if the object is physical, has moved recently, or has been rezzed recently. The engine will ignore teleports containing this flag unless it has been set to "Action Mode"._

-	**Return Data** - _Data about the origin of the teleport inform the Engine if the user is allowed to use the Engine "<<BACK" button to return back to return back to the teleporter. Also included is the specified return landing position set by the owner of the teleporter. These return teleports are one-time consumable TPs which teleport the teleportee back to where they teleported from (Unlike SL's back function which TPs you to the last place you teleported TO). Upon return TP, the ticket is consumed, and teleporters can opt to not allow returnTPs entirely, thus preventing exploiting of the return function in builds or cases where the user should be unable to do so._

-	**Message** - _The datapacket can also contain a string message which is communicated to the Engine user via llOwnerSay(); upon teleport. The included teleporter script does now allow for messages and instead this must be called via API. This choice was made to prevent common teleporters from contributing to the existing barrage of messages we get sent to us in chat as we travel the grid. Some 1st party scripts and 3rd party Scripts using the API will be able to send a message if they so please however. _

### Execution of the Datapacket
Once processed, the datapacket is then executed if the attached Engine's access settings (Execute commands from Any/Group+Owner/Owner only) permit it.

The datapacket and its in-the-background security is the core feature of the Engine, making it not only easy to use but safe to have attached 24/7 and open enough to be used in a wide range of cases as per the needs of script calling the teleport.

The result is a more immersive user-experience and a new approach to how we do teleports in Second Life (asuming TPEngines become as wide spread as Animation Overriders).


## Doesnt this exist already?

A scripted attachment to serve as a system for facilitating teleports from scripted objects?  
Why not just use Experience?  
Doesn't RLV do this already?  

### Part 1: "But what about Experience?..."

Experience is a powerful tool in Second Life that has greatly expanded what we think of as possible with LSL, but as great a thing it is, it does have some serious limitations.	
-	**Paywall** - _Experience exists behind a paywall, requiring Premium to create and compile scripts that use Experience._

-	**Locked down** - _Experience scripts must be compiled to run with a specific Experience and that specific Experience must be allowed to run on land._

-	**Performance Bottleneck** - _Experience offers some great possibilities via llCreateKeyValuePair()/llReadKeyValuePair() but this requires a Dataserver response for reading and writing of data which turns this into a trade off of speed vs ease of scripting._

These limitations don't really impact usecases for the likes of full-sims that seek to create a managed user-experience, which appears to be the intended purpose for Experience.

However, it does leave more broad brush general purpose cases like your every day SitTP or MapTPs out in the cold and stuck in a groundhog day like experience re-living 2006 scripting every time you use one. They work, but they can be immersion breaking or unintuitive solutions. Something better has been very much needed for a good while.

Good for regions seeking to create a carefully constructed immersive user experiences, bad for day to day general purpose use.

### Part 2: "...Isn't that what RLV is for?"

Restrained Life Viewer (RLV) does indeed offer some of this functionality, while offering a whole lot more ontop of it, but RLV itself has its own flaws.
-	**Wide Scope Permissions** - _RLV works based off interaction with a compatible viewer acting as a bridge to allow scripted objects to perform actions on the viewer itself. The issue with this is this grants all permissions as a starting point then picks and chooses which are needed. This puts the balance of power in the creator, not the user (Though this is by design considering RLV's origins)._

-	**Dangerous to leave "Open"** - _RLV makes significant useage of Allow/Disallow lists to control who can and cannot execute certain RLV functions. This means for a general purpose system, this needs to be left in an open state (potentially with the addition of a Blacklist) which while an easy solution, leaves users vulnerable. As a result, its difficult for an RLV system to serve a passive role in the background if its built for a general purpose approach. This results in RLV being often time very specific and locked down to working in specific expected ways as this approach to development is encouraged instead._

-	**Breaks the Sandbox** - _As mentioned earlier, RLV works via interaction with a viewer, as a result the sandboxed environment seperating your viewer from the world you're interacting with is diminished, asking of the user an element of trust as part of its use. Something that many are comfortable with, but for those not comfortable with this leaves them out in the cold when it comes to more immersive experiences._

-	**Uses non-native scripting** - _RLV makes use of scripting that isn't native to the Linden Library in LSL. While common viewers like Firestorm do support this out the box, these are not enabled by default and mean without RLV being enabled in the user's viewer they won't get access to the functionality it provides. While the same can be said of an attachment, Requiring users to enable settings in preferances adds an extra step that doesn't make inherent sense for a user who has not yet encountered RLV, again in turn limiting RLV to bespoke solutions instead of open general purpose ones._

RLV as a result is simlutaneously overkill for teleportation but at the same time inherently undermined via a chilling effect that comes from the need to balance being open enough for daily use while locked down enough to prevent abuse of the RLV system and not a true native solution.
Good for bespoke solutions like the nanite system or BDSM sex beds, bad for open general purpose solutions.

# Additional Modules

## Multi-Mode LM Teleporter Script (Free and Included with the Teleporter Engine Box)

The base Teleport engine is free and includes a script with which you can use to make your own teleporters or convert your existing teleporters over to the Teleport Engine.

### Features

-	**Provides Legacy Support** - _Since the Engine is not wide spread as of yet given it's recency, the included teleporter script also does SitTP and MapUI TP while attempting to improve these legacy teleport methods as best as can be done for 2018. The SitTP mode will adjust as needed in its method of operation for destinations over 300m from the teleporter and will automatically determine if the destination is off-sim, switching to MapUI/HUD mode without the user needing to manually do so. SitTP and MapUI Tp modes also provide support for the Engine at the same time, so that you can get the benefit of the Engine while non-engine users can still use your teleporters. (A giver is included with the Teleport Engine and a sign you can use to inform visitors to your land the BunBox Teleport Engine is in use and give them a copy.)_

-	**Access Settings** - _The included teleporter script allows you to restrict access to your teleporter based on Owner only, Group+Owner or Allow all. (Default: Group+Owner)_

- 	**Touch** - _Touch activation can be disabled or a maximum range for activation can be set. (Default: Touch ON, Range NO LIMIT)_

- 	**Collision** - _Collision activation can be disabled or the object can be set to phantom activation. (Default: Collision ON, Phantom OFF)_

-	**HUD -> Sound** - _Toggle SoundOnTP or set a sound to be played on TP by the Engine when using the teleporter by UUID. (Default: Sound ON, UUID 939be5c6-64bb-4f96-4cac-25accfc26177)_

-	**HUD -> Return** - _Toggle ReturnTP allowed/disallowed or change the position ReturnTPrs will land at (Position is set to where you are standing) (Default: Return ON, Return Position OBJECT POSITION+<0,2,0>)_

### Useage

- Just drop the script into an object you wish to act as a teleporter and add a Landmark to your destination into the object's contents.  

- Pick which mode the teleporter should work in from the pop up, then you're good to go!  

- Although you can further configure the teleporter from the menu that shows up. _(Long click the teleporter to make this re-appear later)_

## Random Sim Teleporter Module (L$249 Copy/No Mod/No Trans)

Teleports yourself and all avatars within 5m with matching active group to a random region in Second Life.

### Features

-	**Integrates with Teleport Engine** - _Only the person initiating the teleport requires the module, everyone wearing a Teleport Engine who is within range and has the same active group will be teleported along with you. ReturnTPs are generated as with any other teleporter, allowing your group to easily regroup back at base. No need for additional attachments._

-	**Integrates with Second Life Groups** - _Your active group controls who will be teleported, Use SL groups to form your group of simhoppers._

-	**Bypass Action Mode checks if on land you own.** - _While the Random Sim TPr can be used anywhere, if used on land you own, the Action Mode checks will be bypassed on participants. Try running sim hops out of your own land or maybe even getting a parcel specifically for running a clubhouse for sim hops and storing tokens of your adventures. I promise you it'll make it a lot more fun._

### Useage

- Attach the module and make sure participants have the same active group and are within 5m.  

- If you are not on land you own, make sure all participants have Action mode enabled _(This will have to be re-toggled after every teleport.)_

- Click the dice to begin the teleport.  

- Long click the dice (1s or more) to silence messages from the module.  

- Silencing persists between attach/detach and login/logouts.

### Support or Contact

You can contact me in-world [BunBoxMomo](https://my.secondlife.com/bunboxmomo?username=bunboxmomo)
