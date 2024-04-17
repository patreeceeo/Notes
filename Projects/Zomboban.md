You just started a new job as a _sokoban_ (warehouse worker) Each day at the job is a new puzzle, and your reward is some BS corporate "we're one big happy family" theater, and the money you need to survive. After your first week, they assemble the new recruits and offer all of you very special helmets. "These helmets let us put our thoughts directly into your head. Neat, eh?" your boss explains. Everyone takes the helmet, but when they come to you, you refuse and then the real game begins. You have to find your way out of the building while dodging the people who want to helmet you. You come back, though, because you need the money and every other job out there has the helmets, too. 

~~A new name? Cheetle World
Story: You work in the offices of Apple-Motorola-Toyota-Sony-Ericsson of America, Inc. You're a diligent worker. Well, as diligent as anyone can expect, because let's face it: It's a bullshit job.

~~Lately, they've been having these seminars and encouraging all employees to attend. Bad vibes! You've managed to steer clear so far, but the people who have been going have been acting weirder than usual, and today, they're actively trying to corner you, for who knows what. But the looks in those eyes says it ain't to chit chat. They're really making it hard for you to do even the bare minimum. So, are you going to get to the bottom of this? Hell no. Let's just get out of here, get to the gig tonight (you're the front-woman of an unsigned psychedelic cow-punk band), and find a new job tomorrow. But if you're going to escape, you're going to need 🅒🅗🅔🅔🅣🅛🅔 🅜🅞🅥🅔🅢.

Story: You've "quiet quit" (a long time ago) and you spend more mental energy trying to figure out how to avoid work than it would require to actually do the work. But that's no fun, is it? Plot out your groovy escapades in this handy simulator.
Story: You're a gig worker. Hey, it's a job, right? Speaking of which, something's been up lately. The fellow office dwellers have been acting more creepy and corporate than usual. If you're going to get through these gigs, you're going to need some CHEEDLE MOVES. Everyone seems to be sizing you up. The Steve's have literally been out to get you, but he's never been too nimble on those roller skates. The Brittany's have been stomping about, but she's easily distracted. The Mungers are omnipresent, but these days they're impressed with anything shinny. Also, it's totally okay to throw stuff, because safety 3rd! 
~~Story: You return from your unauthorized vacation, half-expecting to be fired, to find that your office mates are behaving strangely. Well, more strangely than usual... Is this related to the "human resource enhancement project" you see mentioned near the top of your work e-mail? ~~

It's got tile-based puzzling reminiscent of Chip's Challenge, with corporate satire a la Stanley Parable, with a psychedelic/underground comix visual aesthetic.

It's as if you're a secret agent up to some corporate espionage, but in reality you're just trying to live your best life under the boot of capitalism.

puzzles as mind-numbing as a corporate job, but a lot more fun!

What if boxes can be stacked on top of each other, and stacks of boxes cannot be moved?

Main character: Cheetle (nickname)

CHEETLE MOVES:
* WASD to move
* Shift+WASD to use next inventory item

Inventory items (in stack)
* paper airplane that you throw to create a distraction
* pogo stick that you use to jump over a box (happens automatically if you have a 1 tile running start and there isn't anything on the other side of the box
* climbing shoes allow you to climb onto boxes (even stacked boxes)
* banana peel that you drop in whatever direction you're facing and when anything walks on it, it will slide until it hits something
* mop can be used to make floors slick.
* keys - throw them at doors of the corresponding color to open them
* fork lift - can be used to stack boxes on top of each other and move stacks of boxes

Non-stack items
coffee - maybe you start with a limited number of moves and you have to pick up coffee to add more moves?

Kinds of tiles:
- Boxes - can be pushed around if there's nothing on the other side of them
- Walls - just block movement
- Thin walls - allow you to enter their tile but block entering from one particular direction (N, S, E, or W)
- Buttons - toggle walls of the corresponding color when there's something on them
- Freshly mopped floors - force you to continue to move in whatever direction you were moving
- Water tiles - Block your movement. You can push boxes into them to cross.
- Conveyer belts - force you to move in whatever direction they're moving
- Bro - Starts walking towards you whenever you have either the same X or Y position, keeps walking in that direction until you have the same X or Y position again or run into something. Forces rewind when lands on player tile. Can be trapped inside boxes.
- Manager A - Paces in one direction until he reaches a wall, then turns 90 degrees until he's unblocked. Will start moving towards anything that's moving and has the same X or Y position. Forces rewind when lands on player tile. Can be trapped inside boxes.
- Intern - Paces in one direction until they reach a wall, then turns 180 degrees. Forces rewind when lands on player tile. Can be trapped inside boxes.
- Manager B - Same as Manager A but turns -90 degrees.
- Executive - Walks along the edges of the walkable area. Starts moving in your direction when you enter the same X or Y position. Keeps moving in that direction. Forces rewind when lands on player tile. Can be trapped inside boxes.
- Regional manager - rides a motorcycle, looks like Elvis, also in a rock band, can move multiple tiles at once but telegrams his moves (motorcycle moves there first, his arms stretch out, then his body moves there)
- light switches - turn everything black, you can't see anything and enemies can't see you. You have to remember how to navigate the space and avoid enemies.
- ??? - Take you to another level.
# sprint 1/1/24

* ~~box on enemy should eliminate it
	* motivation: It's inevitable that a box can end up on the same square as a moving entity. I like making it a loose condition when that happens to the player, so it would only make sense that it's a way to defeat enemies.
	* estimate: 35min
	* start: 3:05
	* changed my mind: I'll try letting enemies hide inside boxes and jump out at the player and see how that goes.
* ~~fix bug: throwables block movement
* ~~create tumblr page
	* motivation: I want to be able to easily share and get feedback on the creative direction of the game. I want to see if other people see the humor, find the ideas interesting, perceive it the way I want them to. I need to get practice with sharing my work and building community around it.
* refactor ActLike component
	* design: Use polymorphic OOP to bind state and behavior directly to the component's value. Create methods that handle various events, such as:
		* another game object is about to start moving
		* another game object is about to stop moving
	* motivation: in order to code the more complex behaviors I have in mind, it'd much easier to switch use polymorphism. The big nested control flow statements are already a bit tough to maintain.
	* plan: spike for 90mins then reflect and plan out the rest.
		* create a minimal Behavior interface
		* refactor ActLike component to accept objects that implement Behavior interface
		* For Player, Bro, Box, Airplane, and Wall
			* create Behavior class while refactoring systems to use behavior object
	* finishing up:
		* events should include a tile range. Event handlers simply filter using the tile range. By default the tile range is the range of tiles visible on screen.
		* the spatial index in the event handlers map is probably overkill.
* create menus using @pixi/ui
	* design: Show the main menu when the game loads. When playing or in normal mode of the editor, user can press ESC to bring up the menu. Menu selections are always stored as URL query string parameters so they're statefully integrated with the browser.
		* main menu:
			* play
			* edit
		* edit menu
			* select level
	* estimate: 3hrs
	* subtasks:
		* create the concept of "scenes" and a "scene manager"
			* design: Before anything happens from the player's perspective, the scene manager must be told what scene to run. A scene knows how to start itself, how to update itself on each frame, and how to dispose of itself to make way for the next scene. The scene / scene manager will subsume the task switcher system and the existing overlay code.
		* figure out how to create sprites/display objects for the menu. Should each element in the menu be its own sprite? If so, then it's properties could be determined by its entity's components. These entities could be added by the scene when it's constructed. Maybe each scene should have a record called "entities" as a field that maps names to entity ids. 
* fix the crash that happens whenever the code is changed such that saved/loaded components that refer to other entities no longer point to the entities they should point to.
	* design: instead of saving the actual entityId, it should save an offset from the highest entityId that existed before loading.
* create title screen
	* design: title screen is displayed when the game loads. Upon input, the main menu is displayed with whatever artistic slight-of-hand that looks good
* create UI chrome for showing inventory
* change/reset level
* work on new sprites
* speech bubbles for hints/tutorial
# sprint 12/13/23
From now on I'll actually start a new sprint each week. Had the playtest at the MADE this past weekend. Got a lot of good feedback and found a lot of bugs.
* ~~take a new screencap of the game in its current state, for posterity.
	* estimate: 15 minutes
* ~~bug: it's possible to place walls on top of player in the editor
* ~~bug: something weird happens when zombies collide with unzombies
* ~~bug: somehow zombies can end up on top of crates
* ~~bug: undo after throwing potion first move causes crash
* ~~bug: throwing a potion doesn't take a turn~~
* improvement: redesign the player character
	* the guy in a suit just isn't the most inspiring hero. I'm leaning towards having it be a girl who's father works in the facility. She's looking for her father who is probably one of the zombies.
* ~~improvement: try having zombies only stop you when they overlap your player.
	* depends on: redesigning the player character
	* motivation: it might make it easier to design puzzles
	* design: use a feature flag to decide to apply this rule. Create an large scale illustration (or even an animation) of the player fighting the zombie to show in the the overlay. 
* ~~improvement: change something so it doesn't seem like you're eating unzombies when you move over them
	* design: show a cutscene? have the unzombie give you some helpful intel?
* ~~Improvement: editor C keybind
	* ~~motivation: B is more intuitive since B can stand for Box or Block. Box is a more common, general word for what the sprite looks like, and Block is a common word used in this genre of game. People at the play test didn't immediately pick up that C stands for Crate. Also Crate sorta sounds like Create, which could be confusing spoken aloud.
	* ~~estimate: 2 minutes 
* ~~improvement: editor W keybind
	* ~~motivation: since changing the editor movement keys to WASD, now the save level keybind (Shift+W) causes the cursor to move up.
	* ~~design: just detect if the shift key is being pressed and don't move the cursor if it is.
	* ~~estimate: 5 minutes
* ~~improvement: simplify undo apparatus (break into smaller chunks)
	* design/motivation: Every entity that can have its state undone has a shadow entity that, when an undo is requested, receives the state for that entity from the top of the undo stack. There are then re-entrant delta-time functions that transition the value of each component on the original entity to the value of said component on the shadow entity. This way we don't have to use velocity or the physics system to undo position, and other components can be added to the undo apparatus in a standardized way. Add an undo system that will query for undo components. (This doesn't actually have to be a component since only the undo system will access this info.) The undo components point to the shadow entity. The system then simply applies the transition function for each component, if necessary. All of the management of the undo stack can also be moved to this system. It can simply expose an API that the game system can use in keybinds. That API:
		* popUndo(ids): pop state from the stack and apply it to the shadow entities (throw an error if the stack is empty)
		* pushUndo(ids): push the state of all undo-able entities onto the stack.
	* estimate: 5 hours to get to where everything in the game can be undone.
	* questions: what if the entity has a non-zero velocity? leave its velocity alone, keep it's displacement limit at zero? how will the system remember the original difference between component A of the shadow entity and component A of the undo entity in order to perform linear interpolation?ja
	* subtasks:
		* ~~remove existing undo code
		* implement enableUndo function
		* implement pushUndo function
* improvement: animate velocity (break into smaller chunks)
	* motivation: will look better and make it easier to tell what's going on, and smooth camera movements might be more comfortable for players.
	* design: Since there's no friction (to allow for projectiles) yet all movement is quantized, there has to be a way of limiting movement due to velocity. The physics system maintains an internal record per-entity record of A.) the per-turn movement limit, in tiles (neglecting difference between X and Y) and B.) how much it's moved in the current turn. With this in place, it should be possible to move entities smoothly using their velocity and the delta time. Will need to make sure to update the tile-based spatial partition only once an entity is fully inside a tile, otherwise, the physics system in its current form will think the entity is colliding with itself. Maybe instead I just make the physics system smarter?
# sprint 11/9/23
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
  * Implement separate puzzles using doorways
	  * design: The game is a collection of (self-contained?) puzzles that fit within a single screen. The camera moves with the player, but only by 1 whole screen at a time, triggered by the player reaching the edge of the screen. Each level has at least one exit that the player can use to progress to a new puzzle, doors simply allow the player to pass through. Sometimes it's possible to see portions of adjacent puzzles?
	  * subtask: edit and render doors
		  * design: Doors need to be face in any of the 4 cardinal directions. Currently there's no concept of orientation. Need to add an orientation component and be able to update it via the editor. After placing an orient-able object in the editor, it automatically enters "orient" mode in which the direction keys can be used to set the orientation of the object under the cursor. You can also press "o" to enter orient mode from normal mode. The orient component is actually a virtual component that changes the LookLike component: Every orient-able object's LookLike value belongs to a mapping from each possible orientation to the corresponding LookLike value.
		  * time: about 4.5 hours
	  * subtask: allow player and pushables to move through doors
		  * design: doors can be rendered on the background layer to simplify rendering. The physics system should exclude doors from collisions. Doors don't need any behavior (yet) so no ActLike component or enum value for them.
		  * estimate: 30min
		  * start: 3:36
		  * finish: 3:41
		  * time: 5 minutes
		  * design: the look of the doors will need to change
	  * subtask: pressing "G" fills the current screen with walls
		  * estimate: 5 minutes
		  * start: 3:45
		  * finish: 4:00
		  * time: 15 minutes
	  * subtask: automatically add a floor tile wherever there isn't a wall
		  * motivation: for now, there's only going to be 1 kind of floor tile so they should be created automatically. However, we need to know when and where they should be placed. This rule is simple and ensures that floor tiles are placed only where needed
		  * design: In edit mode, on every frame, iterate through tiles on the current screen, add floor tiles where needed, remove them where they aren't.
		  * estimate: 15 minutes
		  * start: 4:01
		  * finish: 4:11
		  * time: 10
	  * subtask: implement camera that moves one screen over when player reaches the edge of the screen
		  * design: create a camera entity that has a camera tag and a position. The render system uses its position to know what entities to render. If an entity is within a half screen width / height, then render it. Initially the camera is positioned at width / 2, height / 2. When the player moves off screen, add/subtract 1 width or height to the camera's position. Also, sprites should be positioned relative to the camera, so subtract the camera's position and add 1/2 screen width or height.
		  * estimate: 1hr
		  * time: 2.5hr?
  * weapons of dezombification
	  * motivation: I want the player to be able to use tools like bombs and guns (that de-zombie-fy the zombies). As opposed to having an inventory system where the player collects and equips themselves with items, maybe these items can just be used wherever they've been placed in the map, and you use them by bumping into them? When used successfully, the targeted zombie becomes a regular human who waits helplessly until the player collects them, adding to their score. How would these objects look? The bomb is pretty obvious. The gun would be on a turret and would rotate and fire in whatever direction the player bumps it? Not being able to collect these items robs the player of the chance to choose where to use them. Maybe at least the bomb should be collectible, in which case I'll need to display how many bombs the player has in the HUD. I think, for now, there should just be ammo that you can collect, you have the gun already. Or maybe you have infinite ammo? Infinite ammo is simpler to implement, so maybe should just go with that for now, and can implement limited ammo + ammo packs later if necessary. 
	  * design: When the user presses the fire key (shift perhaps?) and a direction key, add the projectile potion entity and give it the corresponding velocity. When it collides with something, remove it. If the thing it collides with is a zombie, turn the zombie into a human. The undo apparatus will need to register where projectiles are created and where they collide along with their velocity.
  * should zombies continue moving in whatever direction they were moving when they last saw the player?
	  * motivation: this would make it possible for zombies to cancel each other out when they collide. Could also be useful for having zombies push blocks for you. In the second case, it would be annoying to have to stay in the zombie's line of sight. This might also make zombies a harder target if we're trying to hit them with something.
  * should zombies be able to push blocks?
	  * motivation: Seems like it would make the puzzles more interesting and dynamic.
	  * design: When the physics system detects a collision between a zombie and a pushable, call the existing attemptPush function.
	  * estimate: 30 minutes
	  * start: 3:27
	  * finish: 4:02
	  * time: 35 minutes
  * should zombies cancel each other out when they collide?
	  * motivation: Seems like an interesting way to solve the problem of how to defeat them. Maybe some puzzles require eliminating some zombies. This conflicts with the idea of de-zombie-fying the zombies. 
  * should zombies be able to move out of turn? No.
  * animate the zombies!
	  * motivation: because animation is fun
	  * design: make every sprite an instance of pixi.AnimatedSprite iff it has a SpriteSheet component. Load the animation data via a sprite sheet JSON file exported from Aseprite.
	  * estimate: 1.5 hours
	  * start: 4:45
	  * finish: 6:30?
	  * time: 1.75 hours?
   * player should be frozen with only the option to undo when they're adjacent to a zombie. It should be a "big moment"
	   * motivation: even though the zombies don't kill you, there needs to be some reason to avoid them, or else they're all bark and no bite, and not really zombies IMO.
	   * design: Detecting when the player is adjacent to a zombie is easy enough, simply ignore any input except undo in that case. Also fade out all other sprites and show text explaining the situation.
	   * estimate: 1hr
	

## backlog
tech ideas:
- system classes using explicit resource management (requires node v20)

creative ideas:
* use isometric (45 degree rotation) tiles?