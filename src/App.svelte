<script lang="ts">
  import { window } from "@tauri-apps/api";
  import {
    LogicalPosition,
    LogicalSize,
    PhysicalSize,
    type Monitor,
  } from "@tauri-apps/api/window";
  import { onMount } from "svelte";
  import { Direction } from "./lib/Direction";
  import Pet from "./lib/Pet.svelte";

  const interval = 350;
  const movementSpeed = 30;
  let positionX = 0;
  let positionY = 0;
  let direction = Direction.FORWARD;

  onMount(() => {
    moveWindow();
  });
  async function moveWindow() {
    await window.appWindow.setSize(new LogicalSize(32,32));
    const monitors: Monitor[] = await window.availableMonitors();
    const monitor = monitors[0];
    const scaleFactor = monitor.scaleFactor;
    const size: PhysicalSize = monitor.size;
    const logicalSize: LogicalSize = new PhysicalSize(size.width, size.height).toLogical(scaleFactor);
    const spriteWidth = 32;
    const spriteHeight = 32;
    setInterval(() => {
      // set movement direction
      if (
        positionX == 0 && 
        positionY == 0) {
        direction = Direction.FORWARD;
      } else if (
        positionX >= logicalSize.width - spriteWidth && 
        positionY == 0) {
        direction = Direction.DOWN;
      } else if (
        positionX >= logicalSize.width - spriteWidth &&
        positionY >= logicalSize.height - spriteHeight
      ) {
        direction = Direction.BACKWARD;
      } else if (
        positionX == 0 && positionY >= 
        logicalSize.height - spriteHeight) {
        direction = Direction.UP;
      }

      // move according to direction
      switch (direction) {
        case Direction.FORWARD:
          positionX += movementSpeed;
          break;
        case Direction.BACKWARD:
          positionX -= movementSpeed;
          break;
        case Direction.UP:
          positionY -= movementSpeed;
          break;
        case Direction.DOWN:
          positionY += movementSpeed;
          break;
      }
      window.appWindow.setPosition(new LogicalPosition(positionX, positionY));
    }, interval);
  }
</script>

<main>
  <Pet {direction} />
</main>

<style>
</style>
