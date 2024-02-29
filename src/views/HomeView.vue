<script setup lang="ts">
import { createInstance } from "@ecgc/ramp";
import { watch, ref } from "vue";
import { config, options } from "@/ramp-config";

const appElement = ref<HTMLElement | null>(null);

watch(appElement, (newVal) => {
  if (newVal) {
    const rInstance = createInstance(appElement.value!, config, options);

    rInstance.$element.component("WFSLayer-Custom", {
      props: ["identifyData"],
      template: `
        <div>
            <span>This is an example template that contains an image.</span>
            <img src="https://i.imgur.com/WtY0tdC.gif" />
        </div>
    `,
    });

    // add export fixtures
    rInstance.fixture.add("export");

    // add areas of interest fixture
    rInstance.fixture.add("areas-of-interest");
  }
});
</script>

<template>
  <main>
    <div
      id="app"
      ref="appElement"
      style="height: 100vh; max-height: -webkit-fill-available"
    ></div>
  </main>
</template>
