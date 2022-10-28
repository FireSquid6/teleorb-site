+++
title = "Week One"
date =  2022-10-23T21:35:38-05:00
weight = 5
+++
Author: FireSquid (Jonathan Deiss)

### 10/17/22 - 10/23/22
The past few weeks have been all fundamental game mechanics or large underlying systems, so this week I decided to take a break from that. A lot of the issues for Alpha 2 are background or lighting related, so I focused on that as well as learning some new skills. 

### Background Tileset
Given how bland the default gray background was, I decided it was time to create an actual background tileset. After around 2 hours, I was able to come up with this:
![](/images/devlog/background_tileset.png)

To create a cave-like atmosphere, I organized the scene tree like such:
![](/images/devlog/background_tree.png)

Each child under the "Level" node had its own modulate, which changes the color of the children nodes. The "Bottom" node had a modulate of (0.3, 0.3, 0.3), the middle (0.5, 0.5, 0.5), and the top (0.7, 0.7, 0.7). This meant that the further "back" an object was, the darker it would appear. This allows the level designer to create effects like this following: 
![](/images/devlog/new_background_preview.png)

Originally, I planned on adding a parallax effect to the background tilesets, but the locked camera caused this to not look good. I may in the future create a custom parallax system that uses the player's position as the focus for the parallax, however I don't know how long that would take.

This basic background tileset may not be a permanent solution, however it will most likely remain in the game until beta.

### Lighting System
The new lighting system was the biggest (and most difficult) accomplishment made this week. 


### Download
There's no new build this week, as the game is too unstable. As always, you can visit the [downloads page](../../download) to download and play the latest stable version. All feedback is greatly appreciated.