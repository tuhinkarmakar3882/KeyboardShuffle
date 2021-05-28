<template>
  <div class="index-page">
    <button @click="shouldShuffle = !shouldShuffle">
      <span v-if="shouldShuffle">Turn off Shuffle</span>
      <span v-else>Turn on Shuffle</span>
    </button>

    <VirtualKeyboard :shouldShuffle="shouldShuffle" />
  </div>
</template>

<script>
export default {
  name: 'Index',

  data() {
    return {
      shouldShuffle: false,
    }
  },

  methods: {
    press(key) {
      this.typedMessage.push(
        this.shiftPressed || this.capslock ? key.shiftedValue : key.defaultValue
      )

      this.shiftPressed = false

      // this.keys = this.shuffleArray(this.keys)
    },

    toggleShiftKey() {
      this.shiftPressed = !this.shiftPressed
    },
    addSpace() {
      this.typedMessage.push(' ')
    },
    addNewLine() {
      this.typedMessage.push('\n')
    },
    addTabChar() {
      this.typedMessage.push('\t')
    },
    toggleCapsLock() {
      this.capslock = !this.capslock
    },

    deleteChar() {
      this.typedMessage.pop()
    },

    shuffleArray(array) {
      for (let i = array.length - 1; i > 0; i--) {
        const j = Math.floor(Math.random() * (i + 1))
        const temp = array[i]
        array[i] = array[j]
        array[j] = temp
      }
      return array
    },
  },
}
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

  main {
    display: grid;
    grid-template-rows: repeat(5, 64px);
    box-shadow: 0 0 4px hsl(0, 10%, 80%);

    section {
      display: grid;

      &.keys-row {
        &:first-child {
          grid-template-columns: repeat(13, 1fr) 1.4fr;
        }

        &:nth-child(2) {
          grid-template-columns: 1.4fr repeat(13, 1fr);
        }

        &:nth-child(3) {
          grid-template-columns: 1.5fr repeat(11, 1fr) 1.5fr;
        }

        &:nth-child(4) {
          grid-template-columns: 1.9fr repeat(10, 1fr) 1.9fr;
        }

        &:last-child {
          grid-template-columns: repeat(3, 1fr) 3fr repeat(3, 1fr);
        }
      }

      button {
        font-size: 16px;
        padding: 0 1rem;
        display: block;
        border: 1px solid hsl(0, 0%, 50%);
        background: hsl(10, 10%, 90%);

        &:hover,
        &:focus {
          background: hsl(0, 0%, 93%);
        }

        &:active {
          background: hsl(0, 0%, 85%);
        }

        &.active {
          background: hsl(154, 59%, 70%);
        }
      }
    }
  }

  pre {
    border: 1px solid hsl(0, 0%, 80%);
    padding: 1rem;
    border-radius: 4px;
  }
}
</style>
