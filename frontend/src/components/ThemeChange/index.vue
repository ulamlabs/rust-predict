<script setup lang="ts">
import { useColorMode } from "@vueuse/core";
import { ColorSwatchIcon } from "@heroicons/vue/outline";
import { themeList } from "./data";
import type { CustomTheme } from "./types";

defineOptions({
  name: "ThemeChange",
});
const mode = useColorMode<CustomTheme>({
  attribute: "data-theme",
  modes: {
    night: "night",
    synthwave: "synthwave",
    halloween: "halloween",
    forest: "forest",
    luxury: "luxury",
    dracula: "dracula",
    autumn: "autumn",
    business: "business",
  },
  initialValue: "night",
});

const changeTheme = (event: MouseEvent, theme: CustomTheme) => {
  const isSameTheme = mode.value === theme;
  try {
    // eslint-disable-next-line @typescript-eslint/ban-ts-comment
    // @ts-expect-error
    if (document.startViewTransition === undefined)
      throw new Error(
        "document.startViewTransition is undefined, please update your browser to the latest version or use a modern browser.",
      );

    const x = event.clientX;
    const y = event.clientY;
    const endRadius = Math.hypot(
      Math.max(x, innerWidth - x),
      Math.max(y, innerHeight - y),
    );
    // eslint-disable-next-line @typescript-eslint/ban-ts-comment
    // @ts-expect-error
    const transition = document.startViewTransition();
    transition.ready.then(() => {
      const clipPath = [
        `circle(0px at ${x}px ${y}px)`,
        `circle(${endRadius}px at ${x}px ${y}px)`,
      ];
      document.documentElement.animate(
        {
          clipPath: isSameTheme ? [...clipPath].reverse() : clipPath,
        },
        {
          duration: 500,
          easing: "ease-in",
          pseudoElement: isSameTheme
            ? "::view-transition-old(root)"
            : "::view-transition-new(root)",
        },
      );
    });
  } catch (error: unknown) {
    console.error(
      `Failed to change theme : ${error instanceof Error ? error.message : ""}`,
    );
  } finally {
    mode.value = theme;
  }
};
</script>

<template>
  <div title="Change Theme" class="dropdown-end dropdown">
    <div tabindex="0" class="btn-ghost btn gap-1 normal-case">
      <ColorSwatchIcon class="stroke-neutral h-5 w-5" />
    </div>
    <div
      class="scrollbar dropdown-content rounded-t-box rounded-b-box bg-base-200 text-base-content top-px mt-16 h-[70vh] max-h-96 w-52 overflow-y-auto shadow-2xl"
    >
      <div class="grid grid-cols-1 gap-3 p-3" tabindex="0">
        <div
          v-for="theme in themeList"
          :key="theme.id"
          class="outline-base-content overflow-hidden rounded-lg outline-2 outline-offset-2 hover:outline"
          :class="mode === theme.id ? 'outline' : ''"
          @click="changeTheme($event, theme.id)"
        >
          <div
            :data-theme="theme.id"
            class="bg-base-100 text-base-content w-full cursor-pointer font-sans"
          >
            <div class="grid grid-cols-5 grid-rows-3">
              <div
                class="col-span-5 row-span-3 row-start-1 flex gap-1 px-4 py-3"
              >
                <div class="grow text-sm font-bold">
                  {{ theme.id }}
                </div>
                <div class="flex shrink-0 flex-wrap gap-1">
                  <div class="bg-primary w-2 rounded" />
                  <div class="bg-secondary w-2 rounded" />
                  <div class="bg-accent w-2 rounded" />
                  <div class="bg-neutral w-2 rounded" />
                </div>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<style scoped>
.scrollbar::-webkit-scrollbar {
  width: 20px;
  height: 20px;
}

.scrollbar::-webkit-scrollbar-track {
  border-radius: 100vh;
  background: #f7f4ed;
}

.scrollbar::-webkit-scrollbar-thumb {
  background: #e0cbcb;
  border-radius: 100vh;
  border: 3px solid #f6f7ed;
}

.scrollbar::-webkit-scrollbar-thumb:hover {
  background: #c0a0b9;
}

::view-transition-old(root),
::view-transition-new(root) {
  animation: none;
  mix-blend-mode: normal;
}

::view-transition-old(root) {
  z-index: 999;
}
::view-transition-new(root) {
  z-index: 1;
}
</style>
~/components/ThemeChange/types
