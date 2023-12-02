# sprint 10/9/23
* basic, stupid level editor persistence
	* design: create a system that converts all component data into JSON strings and saves them in browser's storage. When booting up, load all components' state.
	* estimate: 45 minutes
	* start: 4:48
	* stopped at: 8:40
	* so much more complicated than I thought... have to persist only particular entities, ~~as well as some metadata about the persisted entities~~. 
	* Also have to think about what entityIds to use for loaded entities. Not all entities are saved, so the engine can create more or less unsaved entities than when the last save occurred. Some of these unsaved entities need to be created before loading the saved entities. Additionally, each component can have a varying set of entities. 
	* The way I've handled this is, when loading, use the series of entityIds starting with the next entityId. This way, existing entities are not clobbered if the engine decides to create more unsaved entities next time, and components that have fewer entities when loading occurs compared to other components will be assigned to the correct entities.
	* start: 10:45
	* finished: 1:16
	* time: ~5.5 hours
	* actually I should refactor this so that all component data and the functions to save and load that data lives in one module. The data for all components can be an associative array keyed by an identifier for the component. Then I won't need to have save functions for each component and the save and load algorithm will be simpler.
	* start: 3:24 11/10
* delete object in editor
	* estimate: 2 hours
	* start: 3:35
	* design: when user presses "d" in normal mode, it tags the entity for deletion. Then systems handle cleaning up the entity before actually deleting it (by removing it from the list of all entities). For example, the render system needs to remove the sprite from the Pixi container. 
	* finish: 4:43
	* time: ~1 hour
* basic, stupid zombie movement
	* estimate: 45 minutes
	* start: 5:00 11/10
	* design: in the editor when user presses 'z' it adds an entity that acts like a zombie, meaning it moves in whatever cardinal direction is closest to the angle the player is relative to the zombie.
	* finish: 5:45
* zombies only move when they can see you
	* estimate: 45min
	* start: 5:57 11/10
	* design: detect if there's an unobstructed line segment between player and zombie and then only apply the existing movement logic if there is.
	* finish: 7:04
	* time: ~1hr
* use a generator for the line function
	* estimate: 10min
	* start: 4:15
	* end: 4:33
	* time: 15min
* improve zombie vision algorithm
	* estimate: 40min
	* start: 4:44
	* motivation: right now the zombie can sometimes see the player when they're on opposite sides of a diagonal line of barrier tiles because the 1 tile width line drawn between them doesn't intersect any barriers. If we make the line between them thicker, then the zombie won't see the player when both the zombie and the player are standing near a vertical or horizontal wall.
	* design: use line segment algorithm 3 times: once directly between the zombie and the player and once on either side of that line. If the center line doesn't intersect a barrier then check the side lines. If both of the side lines intersect then the zombie can't see the player. Where to draw the sidelines: If the line is more or less vertical, then to the left and right. If the line is more or less horizontal, then above and below. If diagonal from top left to bottom right, then one line below and one line to the right...
	* eh maybe it's not that important
	* stop: 5:44
	* re-design: actually there's a much simpler method. Just search the 4 tiles in the cardinal directions from each tile on the line, excluding the first and last tile. If there's more than one of these tiles with a barrier then the line is blocked.
	* start: 10:00
	* stop: 10:50
	* time: ~2hrs
* have zombie movement follow the line between player and zombie
	* motivation: simpler code. If we already generate the line then we don't need the other code controlling the zombie's movement.
	* design: get the line segment generator and call it's next method
	* estimate: 10minutes
	* start: 10:55
	* finish: 12:25
	* time: 1.5hrs
	* explanation: forgot that the implementation of Bresenham's algorithm I was using sometimes draws the line from x1,y1 to x0,y0 instead of x0,y0, to x1,y1 so I had to adapt the code to always start from x0,y0
* add ability to restart level without refreshing the page
	* motivation: player will need to be able to restart the level when they get stuck, also it'd speed up development. I haven't decided yet if player should die when they touch a zombie, but when I do, I'll be able to leverage this same function.
	* design: delete all entities then reload from storage
	* estimate: 30min
	* start: 3:30
	* finish: 4:15
	* time: 45min
* add ability for player to move diagonally
	* motivation: since zombies follow the line from them to player 1 step at a time, they can move diagonally. Thus they can move faster than players when moving diagonally. This just feels wrong. Another solution could be to bring back the alternating x/y movement for zombies, but I think the ability for players to move (and push things) diagonally might open up some interesting possibilities.
	* design: simply iterate through the key map for player movement and test each key if it's down and if so apply that movement.
	* estimate: 15min
	* start: 4:23
	* stop: 4:37
	* this made me realize there's a glitch in the collision handling for diagonally moving entities
	* start: 9:50
	* finish: 11:30
	* total: ~2hr
* add tests for zombie vision
	* motivation: there's still edge cases where the zombie can see but shouldn't. It's hard to test manually. The tests I just wrote for collision handling give me an idea. 
	* design: write a function that takes a 2d array where each element contains an ActLike value with at least a player and a zombie and maybe some barriers and pushables and as a second arg, a boolean for whether the zombie should be able to see the player.
	* estimate: 30min
	* start: 12
	* finish: 1:30
	* time: 1.5hrs
	* I was just thinking about the time to write the test helper function, not the time to write all the tests and fix any bugs found. It's nearly impossible to estimate the latter kind of task.
* add a slight delay to processing player movement keyboard input
	* motivation: diagonal movement requires pressing 2 keys at once, but if there's a slight delay between when the player presses those 2 keys, then the game will process just one of the key presses, resulting in a non-diagonal movement. I don't want the game to be about the player's ability to press keys at the same instant.
	* estimate: 40min
	* start: 3:20
	* design: detect if the set of moment keys pressed this time are the same as the set of keys pressed last time, and if so, then process the movement.
	* finish: 3:40
	* time: 20min
* push pushables
	* motivation: it's a sokoban!
	* estimate: 40min
	* start: 3:42
	* design: detect when a player's movement would collide with a pushable, and when it does then set the pushable's velocity equal to that of the player
	* the devil's in the details. Have to adjust collision handling logic to only prevent the player from moving when there's a barrier in their way (not just a pushable), which means I had to adjust the raster ray trace function to accept an extra parameter telling it what kind of objects to look for.
	* stop: 4:50
	* start: 12:00
	* stop: 1:30
	* start: 2:15
	 * finish: 3:15
	 * time: ~3.5hrs
	 * automated testing FTW. It all becomes much clearer when you focus on one specific case at a time. Was struggling a bit to figure out how to handle when there's a pushable thing being pushed into another pushable thing. Seemed recursive, and it sorta is, but in a very limited way: The physics function can call itself when a pushable is being pushed by a player to determine what that pushable should do.
 * switch to vite
	 * motivation: parcel keeps acting up. It doesn't always rebuild when I make changes, the dev server hangs...
	 * design: create a vite project using its official project scaffolding tool then moving things over.
	 * estimate: 30min
	 * start: 3:20
	 * finish: 4:00
	 * time: 40min
	 * the only reason it took me longer than 20 minutes is my cats were being very distracting
 * research ways to build cross-platform apps
	 * motivation: I might want to offer free and paid versions. The free version would just be available on the web, while the paid version would add some features and only be available for download. Maybe this isn't high priority right now. But I should perhaps start working on it now because there might be some gotchas that I won't discover until I try and the longer I wait the more costly it could be in terms of changing my code to be compatible.
	 * budget: 1hour
	 * start: 2
	 * finish: 3
	 * pretty easy, actually! did notice some an occasional rendering issue. The window would flash black for a split second. Could be because it's running in webkit instead of in chromium.
 * have compiler require units with certain numerical values
	 * motivation: yesterday I spent almost 30 minutes tracking down a bug where I used a number in tile units rather than pixel units or something like that. It wouldn't be hard to create an opaque type and a function that takes a plain number and returns a number wrapped in the opaque type. Can the number still be used in arithmetic? Yes.
	 * estimate: 25min
	 * start: 4
	 * finish: 5
	 * time: 1hr
	 * took a bit longer than expected. There were a few small gotchas, like the resulting type of using the opaque types in arithmetic operations is number, not the opaque type
 * use larger tiles that overlap slightly to create the illusion of depth.
	 * motivation: the 32x32 sprites look fine, but I can make better sprites at 64x64 (ish) and it's actually easier at that resolution. Also I think the 3D effect would like cool. The game needs to look good in order to be marketable.
	 * design: use 64x72 sprites. Layer them such that the bottom sprites are at the top, because they are actually slightly closer to the viewer in the virtual 3D space. That space is divided into 64x64x64 pixel voxels, each occupied by 1 or more sprites. Sprites that fill the entire voxel (such as walls and crates) are draw from the top to the bottom and from the left edge to the right edge. Sprites that are fill only the lower part of the voxel (such as floor tiles) have transparent pixels at the top. Sprites that are tall and narrow (such as people) have transparent pixels at the bottom and to the left and right.
	 * estimate: 90min
	 * start: 4:30
	 * ok this is more complicated than I realized because the render system uses a separate particle container for each unique texture. So in order to maintain that optimization while also allowing sprites to have a z-index that corresponds to their tile Y value, we'll need to create a separate container for each tile Y value. So the full structure would be A.) there's one container per Layer, B.) within each Layer's container, there's on particle container for each Y tile value. C. Within each of those containers, there's a particle container for each unique texture.
	 * finish: 8:30
  * undo moves
	  * motivation: it's more fun if you don't have to restart every time you make a mistake
	  * design: add a system that remembers the movements for all movable entities. The data would need to be sequential. Each item in the sequence would contain a list of entities and their movement. When the user wants to undo, the system removes the last item from the sequence and undoes the movements for each listed entity.
	  * estimate: 1hr
	  * forgot to track time, but I've already worked on it for about 5hrs
	  * why is it so much more time consuming than expected? I haven't really figured out why yet but there are some subtle bugs to this that I haven't been able to isolate despite writing what seems to me like a pretty comprehensive test suite.
	  * time: about 8hrs?
	  * realized that the undo state needs to store the positions, but it needs to apply that state by setting velocities.
  * optimize rendering
	  * motivation: there's pretty bad rendering artifacts in the Tauri build. I'd like to spend a little time with some low-hanging fruit in the render system so that I can test in Tauri without having to look at that ugliness. The architecture of the render system isn't going to change from here on out, so might as well optimize it.
	  * design: The two optimizations I have in mind are A.) only use the layered tile Y-keyed particle containers on the object layer, since that's the only layer that needs the 3d effect. The other layers can simply be a single full-screen particle container. B.) Use a renderDirty tag component instead of a single dirty flag for the whole system. That way the render system does much fewer iterations. For both A.) and B.) write tests first. The tests will actually test a highly parameterized function that will be factored out of the current render system. The parameters will be used to determine the side-effects so that it can be tested. For example, one of the parameters would be a function for creating particle containers and adding them to the scene graph. The actual render system would pass in a function that creates actual particle containers and adds them to the actual scene graph. The tests would pass in a function that creates a plain object and adds it to an array within nested arrays representing the scene graph.
	  * estimate: 4hr
	  * start: 10:54
	  * finish: 3
	  * time: 4hr (!) 
  * create integration test suite that simulates keyboard input. No need for selenium since this game can be played just with keyboard? Tests can make assertions against the ECS.
	  * design: Actually this would probably best be implemented as tests for the GameSystem?
  * zombies can only see and move and attack in whatever direction they're facing. they turn using special spin-y tiles.
	  * Done with this for now. Idk how long it took because life...
	  * Haven't implemented the ability for entities to face a certain direction yet.
  * Add ability to load level data in the SOK format
  * Save and load level data from a file, rather than local storage.
	  * motivation: local storage can be cleared accidentally. And sometimes I have to clear it to clear the level for various development purposes. If it were saved in a file I could get it back easily. Also will want to experiment with many variations of level designs.
	  * design: Dynamically load level from a particular endpoint over HTTP. The endpoint simply sends over the contents of the file. For now the format can be the same JSON string that's stored in local storage. 

## backlog
tech ideas:
- system classes using explicit resource management (requires node v20)

creative ideas:
* use isometric (45 degree rotation) tiles?