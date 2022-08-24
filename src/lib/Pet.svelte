<script>
  import { Direction } from "./Direction";

  export let direction;
  let backgroundX = 0;
  let backgroundY = -32;
  const interval = 200;

  setInterval(() => {
    // pick sprite
    switch (direction) {
      case Direction.FORWARD:
        moveForward()
        break;
      case Direction.BACKWARD:
        moveBackward()
        break;
      case Direction.UP:
        moveUp()
        break;
      case Direction.DOWN:
        moveDown()
        break;
    }
  }, interval);

  function moveForward() {
    backgroundX -= 32;
    backgroundY = -32;
  }

  function moveBackward() {
    backgroundX -= 32;
    backgroundY = -96;
  }

  function moveUp() {
    backgroundX -= 32;
    backgroundY = -64;
  }

  function moveDown() {
    backgroundX -= 32;
    backgroundY = 0;
  }
</script>

<div id="pet">
  <p
    id="sprite"
    style="background: url('src/assets/stardew_cat_spritesheet.png') {backgroundX.toString()}px {backgroundY.toString()}px; width: 32px; height: 32px;"
  />
</div>

<style>
</style>
