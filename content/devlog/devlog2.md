+++
title = "Devlog 2"
date =  2022-11-02T22:45:38-05:00
weight = 5
+++

### 10/31/22 - 11/6/22
Continuing the push to alpha 2, the key recent improvements have been:
- Input hint system
- A more refined jump
- Various developer experience improvements
  
### 🎮 Input Hint System
Many times in games, it's helpful to show the player a "preview" or "hint" of what button they need to press to perform a certain action. I figured I would need to do this a lot in the future, so a dedicated system for doing this would come in handy.

![](/videos/devlog/input_hint.gif)

This system was a lot of work for little payoff. I ended up bodging together [an entire addon](https://github.com/firesquid6/quick-hint) over the course of four or so hours split in between two days. Any `InputEvent` can be sent into a special singleton that will load in a texture.

### 🧍‍♂️ Refined Jump
Jumping now feels less like controlling a wet towel. I found it much easier to define the player's jump using the following variables:
- `jump_height`
- `jump_time_to_peak`
- `jump_time_to_descent`

These variables are then used to calculate gravity, jump_spd, etc. I found this system **WAY** easier than the prior method of editing ambiguous `jump_spd`, `jump_time`, etc. variables. I used [this video](https://www.youtube.com/watch?v=IOe1aGY6hXA) from Pefeper as a guide for making this. If anyone is curious as to what the exact source code looks like, take a look at [player.gd](https://github.com/FireSquid6/teleorb/blob/main/src/player/player.gd) (this file may be different if you're accessing it in the future).


### 🛠 gdvm
I've also started working on a new project: [gdvm](https://github.com/firesquid6/gdvm). This is similar to nvm (node verion manager), but for Godot versions. It's currently being built in Python using Typer and Poetry, both of which I'm new to. If you have experience in either of those libraries, help would be greatly appreciated.
### 👨‍💻 Various DX Stuff
- Screenshot system (not functioning due to Godot 4 issues)
- Better Issue templates

### 🔽 Download 
No new download. Next week? Fingers crossed?