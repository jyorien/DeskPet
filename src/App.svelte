<script lang="ts">
  import { window } from "@tauri-apps/api";
  import { LogicalPosition, LogicalSize, PhysicalSize, type Monitor } from "@tauri-apps/api/window";
  import { info } from "tauri-plugin-log-api";
  import { onMount } from "svelte";
  import Pet from "./lib/Pet.svelte";

  const interval = 350;
  let positionX = 0;
  let positionY = 0;
  // setInterval(() => {
  //         positionX += 4;
  //         if (positionX >= size.width) positionX = 0;
  //         window.appWindow.setPosition(
  //           new LogicalPosition(positionX, positionY)
  //         );
  //       }, interval);
  onMount(() => {
    moveWindow();
  });
  async function moveWindow() {
    const monitors: Monitor[] = await window.availableMonitors();
    const monitor = monitors[0]
    const scaleFactor = monitor.scaleFactor
    const size: PhysicalSize = monitor.size
    const logicalSize : LogicalSize = new LogicalSize(size.width / scaleFactor, size.height / scaleFactor)
    setInterval(() => {
      if (positionX >= logicalSize.width) positionX = 0;
      positionX += 4;      
      window.appWindow.setPosition(new LogicalPosition(positionX, positionY));
    }, interval);
  }
</script>

<main>
  <Pet />
</main>

<style>
</style>
