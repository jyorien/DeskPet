<script lang="ts">
  import { window } from "@tauri-apps/api";
  import {
    LogicalPosition,
    LogicalSize,
    PhysicalSize,
    type Monitor,
  } from "@tauri-apps/api/window";
  import { onMount } from "svelte";
  import Pet from "./lib/Pet.svelte";

  const interval = 350;
  const movementSpeed = 4
  let positionX = 0;
  let positionY = 0;
  let isBackward = false;

  onMount(() => {
    moveWindow();
  });
  async function moveWindow() {
    const monitors: Monitor[] = await window.availableMonitors();
    const monitor = monitors[0];
    const scaleFactor = monitor.scaleFactor;
    const size: PhysicalSize = monitor.size;
    const logicalSize: LogicalSize = new LogicalSize(
      size.width / scaleFactor,
      size.height / scaleFactor
    );
    setInterval(() => {
      if (positionX >= logicalSize.width) {
        isBackward = true;
      } else if (positionX == 0) {
        isBackward = false;
      }
      if (isBackward) positionX -= movementSpeed; else positionX += movementSpeed;
      window.appWindow.setPosition(new LogicalPosition(positionX, positionY));
    }, interval);
  }
</script>

<main>
  <Pet {isBackward} />
</main>

<style>
</style>
