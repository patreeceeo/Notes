Define the overall configuration with a `Phaser.Game` instance. Example:

```javascript
import * as Phaser from 'phaser';

class MyScene extends Phaser.Scene {
  preload () {
    this.load.image('ball', 'assets/images/ball_32_32.png');
  }
  create () {
    // create a sprite
    const ball = this.physics.add.sprite(
      400, // x position
      565, // y position
      'ball' // key of image for the sprite
    );
    // create a group
    const violetBricks = this.physics.add.group({
      key: 'brick1',
      repeat: 9,
      immovable: true,
      setXY: {
        x: 80,
        y: 140,
        stepX: 70
      }
    });
  }
  update () {
  }
}

const game = new Phaser.Game({
  type: Phaser.AUTO, // try WebGL, fallback to Canvas
  parent: 'game', // element ID
  width: 800,
  height: 640,
  scale: {
    mode: Phaser.Scale.RESIZE,
    autoCenter: Phaser.Scale.CENTER_BOTH
  },
  scene: MyScene,
  physics: {
    default: 'arcade',
    arcade: {
      gravity: {x: 0, y: 0},
    },
  }
});
```

### physics world
#### check bounds
```javascript
this.physics.world.bounds.width;
this.physics.world.bounds.height;
```
### collision detection/resolution
```javascript
this.physics.world.checkCollision.<direction> = false;
this.physics.add.collider(spriteA, spriteB, handleCollision, null, this);
```
where `<direction>` is left, right, up or down
#### misc physics
```javascript
sprite.setImmovable(true);
```

### arcade physics sprites
```javascript

const sprite = this.physics.add.sprite(
		400, // x position
		565, // y position
		'ball' // key of image for the sprite
)
sprite.countActive();
sprite.set<dimension>(<number>);
sprite.setVelocity<dimension>(<number>);
sprite.setCollideWorldBounds(true);
sprite.setBounce(1, 1);
```
where `<dimension>` is X or Y

### input
track cursor keys
```javascript
cursors = this.input.keyboard.createCursorKeys();
cursors.<key>.isDown
```
where `<key>` is up, down, left, right, shift or space

### display text
```javascript
const text = this.add.text(
  this.physics.world.bounds.width / 2,
  this.physics.world.bounds.height / 2,
  'Press SPACE to Start',
  {
    fontFamily: 'Monaco, Courier, monospace',
    fontSize: '50px',
    fill: '#fff'
  },
);

// set the transform origin to the center
text.setOrigin(0.5);
text.setVisible(false);
```


### Hot Module Replacement

NOTE: it's critical to destroy the old `Phaser.Game` instance in the dispose callback for HMR to work correctly.

```javascript
game.destroy(true);
```

# Tilemap

`this.make.tilemap(...)` => `ParseToTilemap(...)` => `new Tilemap(...)` => 
# References
- https://stackabuse.com/introduction-to-phaser-3-building-breakout/