# Documentation Under Construction

# BunBox Teleport Engine
## Introduction

Thank you for your interest in the BunBox Teleport Engine.

This site serves as documentation for the Engine, providing explanation of core features, useage in greater detail and example use cases.

## Doesnt this exist already?

A scripted attachment to serve as a system for facilitating teleports from scripted objects?  
Why not just use Experience?  
Doesn't RLV do this already?  

### Part 1: "But what about Experience?..."

Experience is a powerful tool in Second Life that has greatly expanded is doable, but as great a thing it is, it does have some serious limitations.	
-	**Paywall** - _Experience exists behind a paywall, requiring Premium to create and compile scripts that use Experience._

-	**Locked down** - _Experience scripts must be compiled to run with a specific Experience and that specific Experience must be allowed to run on land._

-	**Performance Bottleneck** - _Experience offers some great possibilities via llCreateKeyValuePair()/llReadKeyValuePair() but this requires a Dataserver response for reading and writing of data which turns this into a trade off of speed vs ease of scripting._

These limitations don't really impact usecases for the likes of full-sims that seek to create a managed user-experience, which appaers to be the intended purpose for Experience.

However, it does leave more broad brush general purpose cases like your every day SitTP or MapTPs out in the cold and stuck in a groundhog day like experience re-living 2006 scripting every time you use one. They work, but they can be immersion breaking or unintuitive solutions. Something better has been very much needed for a good while.

### Part 2: "...Isn't that what RLV is for?"

Restrained Life Viewer (RLV) does indeed offer some of this functionality, while offering a whole lot more ontop of it, but RLV itself has its own flaws.
-	**Wide Scope Permissions** - _RLV works based off interaction with a compatible viewer acting as a bridge to allow scripted objects to perform actions on the viewer itself. The issue with this is this grants all permissions as a starting point then picks and chooses which are needed before releasing the unused ones. This puts the balance of power in the creator, not the user._

-	**Dangerous to leave "Open"** - _RLV makes significant useage of Allow/Disallow lists to control who can and cannot execute certain RLV functions. This means for a general purpose system, this needs to be left in an open state (potentially with the addition of a Blacklist) which while an easy solution, leaves users vulnerable. As a result, its difficult for an RLV system to serve a passive role in the background if its built for a general purpose approach. This results in RLV being often time very specific and locked down to working in specific expected ways as this approach to development is encouraged instead._

-	**Breaks the Sandbox** - _As mentioned earlier, RLV works via interaction with a viewer, as a result the sandboxed environment seperating your viewer from the world you're interacting with is diminished, asking of the user an element of trust as part of its use. Something that many are comfortable with, but for those not comfortable with this leaves them out in the cold when it comes to more immersive experiences._

RLV as a result is simlutaneously overkill for teleportation but at the same time inherently undermined via a chilling effect that comes from the need to balance being open enough for daily use while locked down enough to prevent abuse of the RLV system.
Good for bespoke solutions, bad for open general purpose solutions.

```markdown
Syntax highlighted code block

# Header 1
## Header 2
### Header 3

- Bulleted
- List

1. Numbered
2. List

**Bold** and _Italic_ and `Code` text

[Link](url) and ![Image](src)
```

For more details see [GitHub Flavored Markdown](https://guides.github.com/features/mastering-markdown/).

### Jekyll Themes

Your Pages site will use the layout and styles from the Jekyll theme you have selected in your [repository settings](https://github.com/BunBox/TeleportEngine/settings). The name of this theme is saved in the Jekyll `_config.yml` configuration file.

### Support or Contact

Having trouble with Pages? Check out our [documentation](https://help.github.com/categories/github-pages-basics/) or [contact support](https://github.com/contact) and we’ll help you sort it out.
