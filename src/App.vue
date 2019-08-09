<template>
  <div id="app">
    <div class="container">
      <img src="/img/pdca.png" class="pdca" :style="pdcaStyle()" />
    </div>
    <div class="ui-container">
      <div class="flex">
        <div>X</div>
        <button type="button" @click="ax = subSpeed(ax)">
          <i class="material-icons">arrow_downward</i>
        </button>
        <button type="button" @click="rotateX = ax = 0">
          <i class="material-icons">stop</i>
        </button>
        <button type="button" @click="ax = addSpeed(ax)">
          <i class="material-icons">arrow_upward</i>
        </button>
      </div>
      <div class="flex">
        <div>Y</div>
        <button type="button" @click="ay = subSpeed(ay)">
          <i class="material-icons">arrow_downward</i>
        </button>
        <button type="button" @click="rotateY = ay = 0">
          <i class="material-icons">stop</i>
        </button>
        <button type="button" @click="ay = addSpeed(ay)">
          <i class="material-icons">arrow_upward</i>
        </button>
      </div>
      <div class="flex">
        <div>Z</div>
        <button type="button" @click="az = subSpeed(az)">
          <i class="material-icons">arrow_downward</i>
        </button>
        <button type="button" @click="rotateZ = az = 0">
          <i class="material-icons">stop</i>
        </button>
        <button type="button" @click="az = addSpeed(az)">
          <i class="material-icons">arrow_upward</i>
        </button>
      </div>
    </div>
  </div>
</template>

<script lang="ts">
import { Component, Vue } from 'vue-property-decorator'

@Component
export default class App extends Vue {
  rotateX = 0
  rotateY = 0
  rotateZ = 0

  ax = 0
  ay = 0
  az = 0

  mounted() {
    setInterval(() => {
      this.tick()
    }, 41)
  }

  tick() {
    this.rotateX += this.ax
    this.rotateY += this.ay
    this.rotateZ += this.az
  }

  addSpeed(speed: number) {
    if (speed >= 80) {
      return speed
    }
    return speed + 1
  }

  subSpeed(speed: number) {
    if (speed <= 0) {
      return speed
    }
    return speed - 1
  }

  pdcaStyle() {
    const transforms: string[] = [
      `rotateX(${this.rotateX}deg)`,
      `rotateY(${this.rotateY}deg)`,
      `rotateZ(${this.rotateZ}deg)`
    ]
    return {
      transform: transforms.join(' ')
    }
  }
}
</script>

<style scoped>
.container {
  position: relative;
  margin-left: auto;
  margin-right: auto;
  transform-origin: 50%;
  transform-style: preserve-3d;
  display: flex;
  align-items: center;
  justify-content: center;
  width: 320px;
  height: 320px;
}

.pdca {
  position: absolute;
}

.ui-container {
  position: absolute;
  right: 0;
  bottom: 0;
  padding: 0.5rem;
}

.flex {
  display: flex;
  align-items: center;
}

.flex > div {
  width: 2rem;
}

button {
  display: inline-block;
  margin: 0.2rem;
}
</style>
