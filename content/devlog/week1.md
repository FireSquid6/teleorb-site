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
The new lighting system was the biggest (and most difficult) accomplishment made this week. I wanted to build a system that would automatically generate a light node with a specific sprite that would light all of the empty tiles, and "fade out" into the walls. If that didn't make sense, here's a demonstration:

A level starts out looking something like this.
![](/images/devlog/no_lighting.png)

Then, a "lightmap" image fills every empty tile with white, and every full tile with black. The white is then "faded" out so that the floor of the walls is visible to the player.
![](/images/devlog/lightmap.png)

Finally, the lightmap is applied over the level to give it a nice effect. In the future, objects such as torches will be added to further sell the atmosphere.
![](/images/devlog/lightmap_generation.png)


This shouldn't have taken as long as it did, but here's the code for it if anyone's curious. It's been through a lot of iterations, so it probably has some optimizations I'm not seeing. If you have any ideas, feel free to submit a PR or an Issue. The code can be found under [src/level_building/world/world.gd](https://github.com/FireSquid6/teleorb/blob/main/src/level_building/world/world.gd)
```gdscript
# generates a light texture based on a speicifc area and layer of a tilemap
# rect2 is in absolute coordinates, not tilemap cell coordinates
# blend controls how fast the light is faded out. lower = slower fade and vice versa
func create_light_texture(rect: Rect2, tilemap: TileMap, layer: int = 0, blend: float = 0.125) -> Image:
    # by default, fill the entire image with black
    var lightmap: Image = Image.new();
	lightmap.create(rect.size.x, rect.size.y, false, Image.FORMAT_RGB8);
	lightmap.fill(Color.BLACK)
	
	var tile_size: Vector2i = tilemap.tile_set.tile_size;
	var start_cell: Vector2i = Vector2i(rect.position) / tile_size;
	var cells: Vector2i = Vector2i(rect.size) / tile_size;
	var used_cells: Array[Vector2i] = tilemap.get_used_cells(layer)
	
	# iterates through the rows and columns of the tilemap, filling any empty tiles
	for column in cells.x:
		for row in cells.y:
			var x_cell: int = start_cell.x + column
			var y_cell: int = start_cell.y + row
			
			var x: int = x_cell * tile_size.x
			var y: int = y_cell * tile_size.y
			
			if !(Vector2i(x_cell, y_cell) in used_cells):
				var pos: Vector2i = (Vector2i(x_cell, y_cell) - start_cell) * tile_size
				
				var fill_rect: Rect2 = Rect2(pos, tile_size)
				lightmap.fill_rect(fill_rect, Color.WHITE)
	
	# fade out the white cells
	var value: float = 1.0 - blend
	while value > 0:
		var pixels_to_color = []
		for x in range(lightmap.get_width()):
			for y in range(lightmap.get_height()):
				var pixel := lightmap.get_pixel(x, y)
				if pixel.is_equal_approx(Color.BLACK) and should_fill_pixel(lightmap, x, y):
					pixels_to_color.append(Vector2i(x, y))
		
		for pixel in pixels_to_color:
			lightmap.set_pixelv(pixel, Color(value, value, value))
		
		value -= blend
	
	return lightmap


# used to check if a pixel should be colored in when "fading out"
# if the pixel itself is white, this function will return the wrong value
func should_fill_pixel(image: Image, x: int, y: int) -> bool:
	var edges = [
		[x - 1, y],
		[x + 1, y],
		[x, y - 1],
		[x, y + 1],
	]
	
    # this code checks the pixel north, east, west, and south of the pixel. If at least one of those is white, the function returns true
	var white_neighbors = 0
	var image_width: int = image.get_width()
	var image_height: int = image.get_height()
	for edge in edges:
		var xx = edge[0]
		var yy = edge[1]
		
		if xx >= 0 and xx < image_width and yy >= 0 and yy < image_height:
			if image.get_pixel(xx, yy).v > 0:
				white_neighbors += 1
	
	return white_neighbors > 0
```


### Download
There's no new build this week, as the game has not hit a new milestone. As always, you can visit the [downloads page](../../download) to download and play the latest stable version. All feedback is greatly appreciated.

As always, if you would like to contribute, the repo is [here](https://github.com/firesquid6/teleorb).