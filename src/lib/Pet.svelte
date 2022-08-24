<script>
    let backgroundX = 0
    let backgroundY = -32
    const interval = 200
    // document.getElementById("sprite").style.backgroundPosition = `${backgroundX}px ${backgroundY}px`
    function animateSprite() {
        backgroundX-=32
        // console.log(backgroundX, backgroundY)
        // if (backgroundX == -128) backgroundX = 0
    }
    setInterval(() => {
        animateSprite()
    }, interval)
</script>

<div id="pet">
    <p id="sprite" style="background: url('src/assets/stardew_cat_spritesheet.png') {backgroundX.toString()}px {backgroundY.toString()}px; width: 32px; height: 32px;"></p>
</div>

<style>
</style>