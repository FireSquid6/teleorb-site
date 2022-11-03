+++
title = "Devlog 2"
date =  2022-11-02T22:45:38-05:00
weight = 5
+++

### 10/31/22 - X/X/X
School has been tough lately, so not much tangible progress has been made.  
  
Continuing the push to alpha 2, the key recent improvements have been:
- Input hint system
- A more refined jump
- Various developer experience improvements
  
### Input Hint System
Many times in games, it's helpful to show the player a "preview" or "hint" of what button they need to press to perform a certain action. I figured I would need to do this a lot in the future, so a dedicated system for doing this would come in handy.

![](/videos/devlog/input_hint.gif)

This system was a lot of work for little payoff. I ended up bodging together [an entire addon](https://github.com/firesquid6/quick-hint) over the course of four or so hours split in between two days. Any `InputEvent` can be sent into a special singleton that will load in a texture.

### Refined Jump


### Various DX Stuff
- Screenshot system
- Better Issue templates
- Better contributor guides
- Better code quality