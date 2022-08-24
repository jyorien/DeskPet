<script>
  export let isBackward = false;
  let backgroundX = 0;
  let backgroundY = -32;
  const interval = 200;
  function moveForward() {
    backgroundX -= 32;
    backgroundY = -32;
  }

  function moveBackward() {
    backgroundX -= 32;
    backgroundY = -96;
  }
  setInterval(() => {
    if (isBackward) moveBackward();
    else moveForward();
    // animateSprite()
  }, interval);
</script>

<div id="pet">
  <p
    id="sprite"
    style="background: url('src/assets/stardew_cat_spritesheet.png') {backgroundX.toString()}px {backgroundY.toString()}px; width: 32px; height: 32px;"
  />
</div>

<style>
</style>
