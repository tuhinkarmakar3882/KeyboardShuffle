<template>
  <div class="index-page">
    <pre>{{ typedMessage.join('') }}</pre>
    <main>
      <section class="keys-row">
        <button
          v-for="key in keys.slice(0, 13)"
          :key="key.id"
          @click="press(key)"
        >
          <span v-if="shiftPressed || capslock">{{ key.shiftedValue }}</span>
          <span v-else>{{ key.defaultValue }}</span>
        </button>

        <button @click="deleteChar">delete</button>
      </section>

      <section class="keys-row">
        <button @click="addTabChar">tab</button>

        <button
          v-for="key in keys.slice(13, 26)"
          :key="key.id"
          @click="press(key)"
        >
          <span v-if="shiftPressed || capslock">{{ key.shiftedValue }}</span>
          <span v-else>{{ key.defaultValue }}</span>
        </button>
      </section>

      <section class="keys-row">
        <button :class="capslock && 'active'" @click="toggleCapsLock">
          caps lock
        </button>

        <button
          v-for="key in keys.slice(26, 37)"
          :key="key.id"
          @click="press(key)"
        >
          <span v-if="shiftPressed || capslock">{{ key.shiftedValue }}</span>
          <span v-else>{{ key.defaultValue }}</span>
        </button>

        <button @click="addNewLine">enter</button>
      </section>

      <section class="keys-row">
        <button :class="shiftPressed && 'active'" @click="toggleShiftKey">
          shift
        </button>
        <button
          v-for="key in keys.slice(37, 47)"
          :key="key.id"
          @click="press(key)"
        >
          <span v-if="shiftPressed || capslock">{{ key.shiftedValue }}</span>
          <span v-else>{{ key.defaultValue }}</span>
        </button>
        <button :class="shiftPressed && 'active'" @click="toggleShiftKey">
          shift
        </button>
      </section>

      <section class="keys-row">
        <button>ctrl</button>
        <button>alt</button>
        <button>cmd</button>

        <button @click="addSpace">space</button>

        <button>cmd</button>
        <button>alt</button>
        <button>ctrl</button>
      </section>
    </main>
  </div>
</template>

<script>
export default {
  name: 'Index',

  data() {
    return {
      keys: [
        { id: '~', defaultValue: '`', shiftedValue: '~' },
        { id: '1', defaultValue: '1', shiftedValue: '!' },
        { id: '2', defaultValue: '2', shiftedValue: '@' },
        { id: '3', defaultValue: '3', shiftedValue: '#' },
        { id: '4', defaultValue: '4', shiftedValue: '$' },
        { id: '5', defaultValue: '5', shiftedValue: '%' },
        { id: '6', defaultValue: '6', shiftedValue: '^' },
        { id: '7', defaultValue: '7', shiftedValue: '&' },
        { id: '8', defaultValue: '8', shiftedValue: '*' },
        { id: '9', defaultValue: '9', shiftedValue: '(' },
        { id: '0', defaultValue: '0', shiftedValue: ')' },
        { id: '-', defaultValue: '-', shiftedValue: '_' },
        { id: '=', defaultValue: '=', shiftedValue: '+' },

        { id: 'q', defaultValue: 'q', shiftedValue: 'Q' },
        { id: 'w', defaultValue: 'w', shiftedValue: 'W' },
        { id: 'e', defaultValue: 'e', shiftedValue: 'E' },
        { id: 'r', defaultValue: 'r', shiftedValue: 'R' },
        { id: 't', defaultValue: 't', shiftedValue: 'T' },
        { id: 'y', defaultValue: 'y', shiftedValue: 'Y' },
        { id: 'u', defaultValue: 'u', shiftedValue: 'U' },
        { id: 'i', defaultValue: 'i', shiftedValue: 'I' },
        { id: 'o', defaultValue: 'o', shiftedValue: 'O' },
        { id: 'p', defaultValue: 'p', shiftedValue: 'P' },
        { id: '[', defaultValue: '[', shiftedValue: '{' },
        { id: ']', defaultValue: ']', shiftedValue: '}' },
        { id: '\\', defaultValue: '\\', shiftedValue: '|' },

        { id: 'a', defaultValue: 'a', shiftedValue: 'A' },
        { id: 's', defaultValue: 's', shiftedValue: 'S' },
        { id: 'd', defaultValue: 'd', shiftedValue: 'D' },
        { id: 'f', defaultValue: 'f', shiftedValue: 'F' },
        { id: 'g', defaultValue: 'g', shiftedValue: 'G' },
        { id: 'h', defaultValue: 'h', shiftedValue: 'H' },
        { id: 'j', defaultValue: 'j', shiftedValue: 'J' },
        { id: 'k', defaultValue: 'k', shiftedValue: 'K' },
        { id: 'l', defaultValue: 'l', shiftedValue: 'L' },
        { id: ';', defaultValue: ';', shiftedValue: ':' },
        { id: "'", defaultValue: "'", shiftedValue: '"' },

        { id: 'z', defaultValue: 'z', shiftedValue: 'Z' },
        { id: 'x', defaultValue: 'x', shiftedValue: 'X' },
        { id: 'c', defaultValue: 'c', shiftedValue: 'C' },
        { id: 'v', defaultValue: 'v', shiftedValue: 'V' },
        { id: 'b', defaultValue: 'b', shiftedValue: 'B' },
        { id: 'n', defaultValue: 'n', shiftedValue: 'N' },
        { id: 'm', defaultValue: 'm', shiftedValue: 'M' },
        { id: ',', defaultValue: ',', shiftedValue: '<' },
        { id: '.', defaultValue: '.', shiftedValue: '>' },
        { id: '/', defaultValue: '/', shiftedValue: '?' },
      ],
      typedMessage: [],
      shiftPressed: false,
      capslock: false,
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
    border-radius: 4px ;
  }
}
</style>
