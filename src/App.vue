<script setup>
const mode = useColorMode({
  modes: {
    // custom colors
    cafe: 'cafe',
  },
}) // Ref<'dark' | 'light' | 'cafe'>

const switchThemeHandelr = () => {
  mode.value = mode.value === 'dark' ? 'light' : 'dark'
}

const el = ref(null)
// `style` will be a helper computed for `left: ?px; top: ?px;`
const { style } = useDraggable(el, {
  initialValue: { x: 340, y: 200 },
})
</script>

<template>
  <header>
    <img
      alt="Vue logo"
      class="logo"
      src="./assets/logo.svg"
      width="125"
      height="125"
      ref="el"
      :style="style"
      style="position: fixed"
    />

    <div class="wrapper">
      <HelloWorld msg="VueUse | useColorMode & useDraggable" />
      <button class="btn" :class="mode === 'dark' ? 'btn-dark' : 'btn-light'" @click="switchThemeHandelr">
        Switch Theme
        <IconSun v-if="mode === 'light'" />
        <IconMoon v-if="mode === 'dark'" />
      </button>
      <button class="btn" @click="mode = 'cafe'">switch Cafe Mode</button>
    </div>
  </header>

  <main>
    <TheWelcome />
  </main>
</template>

<style>
header {
  line-height: 1.5;
}

.logo {
  display: block;
  margin: 0 auto 2rem;
  cursor: grab;
}

@media (min-width: 1024px) {
  header {
    display: flex;
    place-items: center;
    padding-right: calc(var(--section-gap) / 2);
  }

  .logo {
    margin: 0 2rem 0 0;
  }

  header .wrapper {
    display: flex;
    flex-direction: column;
    place-items: flex-start;
    flex-wrap: wrap;
  }
}

.btn {
  margin-top: 1rem;
  padding: 0.75rem 1.25rem;
  border: none;
  cursor: pointer;
  display: flex;
  justify-content: center;
  align-items: center;
}
.btn-light {
  background: white;
  color: var(--color-heading);
  border: 1px solid var(--color-heading);
}

.btn-dark {
  background: var(--color-heading);
  color: white;
  border: 1px solid var(--color-heading);
}
.btn > svg {
  margin-left: 0.5rem;
}

html.dark {
  background: #282828;
  transition: background-color 0.5s;
}

html.light {
  background: white;
  transition: background-color 0.5s;
}

html.cafe {
  filter: sepia(0.9) hue-rotate(315deg) brightness(0.9);
}
</style>
