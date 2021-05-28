<template>
  <div class="index-page">
    <button @click="shouldShuffle = !shouldShuffle">
      <span v-if="shouldShuffle">Turn off Shuffle</span>
      <span v-else>Turn on Shuffle</span>
    </button>

    <VirtualKeyboard :should-shuffle="shouldShuffle" />
  </div>
</template>

<script>
import VirtualKeyboard from "../components/VirtualKeyboard";

export default {
  name: "Index",
  components: { VirtualKeyboard },
  data() {
    return {
      shouldShuffle: false
    };
  }
};
</script>

<style lang="scss" scoped>
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

.index-page {
  display: flex;
  align-items: center;
  justify-content: center;
  flex-direction: column;
  gap: 24px;
  height: 100vh;
  padding: 1rem;
}
</style>
