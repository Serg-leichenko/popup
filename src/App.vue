<template>
  <div id="app">
    <button id="show-modal" @click="showModal = true">Show Modal</button>

    <Popup v-if="showModal" @close="showModal = false" />
  </div>
</template>

<script>
import Popup from "@/components/Popup";
export default {
  name: "App",
  components: {
    Popup,
  },
  data: () => {
    return {
      showModal: true,
    };
  },
};
</script>

<style lang="scss"></style>
