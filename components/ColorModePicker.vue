<template>
  <div>
    <ul>
      <li v-for="color of colors" :key="color" @click="$colorMode.preference = color">
        <component
          :is="`icon-${color}`"
          :class="getClasses(color)"
          @click="$colorMode.preference = color"
        />
      </li>
      <ColorScheme placeholder="..." tag="span">
        <p>
          Color Mode: <b>{{ $colorMode.preference }}</b>
          <span v-if="$colorMode.preference === 'system'">
            (<i>{{ $colorMode.value }}</i> mode detectado)
          </span>
        </p>
      </ColorScheme>
    </ul>
  </div>
</template>

<script>
import IconSystem from '@/assets/icons/system.svg?inline'
import IconLight from '@/assets/icons/light.svg?inline'
import IconDark from '@/assets/icons/dark.svg?inline'
import IconSepia from '@/assets/icons/sepia.svg?inline'

export default {
  components: {
    IconSystem,
    IconLight,
    IconDark,
    IconSepia
  },
  data () {
    return {
      colors: ['system', 'light', 'dark', 'sepia']
    }
  },
  methods: {
    getClasses (color) {
      if (this.$colorMode.unknown) {
        return {}
      }
      return {
        preferred: color === this.$colorMode.preference,
        selected: color === this.$colorMode.value
      }
    }
  }
}
</script>

<style scoped>
  .feather {
    position: relative;
    top: 0px;
    cursor: pointer;
    padding: 7px;
    background-color: var(--bg-secondary);
    border: 2px solid var(--border-color);
    margin: 0;
    border-radius: 5px;
    transition: all 0.1s ease;
  }
  .feather:hover {
    top: -3px;
  }
  .feather.preferred {
    border-color: var(--color-primary);
    top: -3px;
  }
  .feather.selected {
    color: var(--color-primary);
  }
  ul {
  list-style: none;
  padding: 0;
  margin: 0;
  }
  ul li {
    display: inline-block;
    padding: 5px;
  }
  p {
    margin: 0;
    padding-top: 5px;
    padding-bottom: 20px;
  }
</style>
