<script setup lang="ts">
import { register } from "@tauri-apps/api/globalShortcut";
import { appWindow, LogicalPosition } from "@tauri-apps/api/window";
import { onMounted, ref } from "vue";
import OverlayWindow from "./components/OverlayWindow.vue";
import { useThrottleFn } from "@vueuse/core";

const triggered = ref(false);

const throttleShow = useThrottleFn(() => {
  triggered.value = true;

  setTimeout(() => {
    triggered.value = false;
  }, 1000);
}, 1000);

onMounted(async () => {
  await register("CommandOrControl+Shift+O", (shortcut) => {
    console.log("Shortcut pressed:", shortcut);
    throttleShow();
  });

  appWindow.setIgnoreCursorEvents(true);
  appWindow.setPosition(new LogicalPosition(0, 0));
  appWindow.setFullscreen(true);
  appWindow.setSkipTaskbar(true);
});
</script>

<template>
  <div class="container">
    <OverlayWindow>
      <template #header>
        <h1>Coucou Vilna</h1>
      </template>
      <div>
        Ca c'est un ptit overlay sympa qui devrait pouvoir rester sur ton
        bureau. Pour fermer, tu peux simplement kill le process :D
      </div>
    </OverlayWindow>

    <OverlayWindow :style="{ display: triggered ? 'block' : 'none' }">
      <template #header>
        <h1>Touché!</h1>
      </template>
      <div>Tu as appuyé sur la touche magique! Bravo!</div>
    </OverlayWindow>
  </div>
</template>

<style scoped>
.container {
  display: flex;
  height: 100vh;
  gap: 1rem;
  flex-direction: column;
}
</style>
