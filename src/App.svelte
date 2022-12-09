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
  const movementSpeed = 5;
  let positionX = 0;
  let positionY = 0;
  let direction = Direction.FORWARD;

  onMount(() => {
    moveWindow();
  });
  async function moveWindow() {
    const monitors: Monitor[] = await window.availableMonitors();
    const monitor = monitors[0];
    const scaleFactor = monitor.scaleFactor;
    const size: PhysicalSize = monitor.size;
    const logicalSize: LogicalSize = new PhysicalSize(size.width, size.height).toLogical(scaleFactor);

    setInterval(() => {
      // set movement direction
      if (
        positionX == 0 && 
        positionY == 0) {
        direction = Direction.FORWARD;
      } else if (
        positionX >= logicalSize.width - 32 && 
        positionY == 0) {
        direction = Direction.DOWN;
      } else if (
        positionX >= logicalSize.width - 32 &&
        positionY >= logicalSize.height - 48
      ) {
        direction = Direction.BACKWARD;
      } else if (
        positionX == 0 && positionY >= 
        logicalSize.height - 48) {
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
