<template>
  <div class="window"
  v-bind:class="{ 'w-min': minimized, 'w-max': maximized }"
  v-bind:style="{left: this.coords.left + 'px', top: this.coords.top + 'px', transition: '0s'}"
  v-on:mousemove="elementDrag">
    <div class="head flex a-i-center j-c-s-between" v-on:mousedown="mouseDown" v-on:mouseup="mouseUp">
      <p>{{header}}</p>
      <div class="flex">
        <div class="circle min" v-on:click="minimizeWindow" v-if="ismin"></div>
        <div class="circle max" v-on:click="maximizeWindow" v-if="ismax"></div>
        <div class="circle close" v-if="isdelete"></div>
      </div>
    </div>
    <div class="body">
      <slot name="window-body">default window body</slot>
    </div>
  </div>
</template>

<script>
export default {
  name: 'sexywindow',
  props: {
    header: { type: String, default: () => '' },
    ismin: { type: Boolean, default: () => true },
    ismax: { type: Boolean, default: () => true },
    isdelete: { type: Boolean, default: () => true },
    x: { type: Number, default: () => 300 },
    y: { type: Number, default: () => 300 }
  },
  mounted () {
    this.coords.left = this.x
    this.coords.top = this.y
  },
  data () {
    return {
      coords: {
        left: 300,
        top: 300,
        last_left: 300,
        last_top: 300
      },

      p: {
        pos1: 0,
        pos2: 0,
        pos3: 0,
        pos4: 0
      },
      minimized: false,
      maximized: false,
      draggable: true,
      mousedown: false
    }
  },
  methods: {
    closeWindow: function () {
      /// / TODO: anus
    },
    minimizeWindow: function (e) {
      this.minimized = !this.minimized
      this.draggable = !this.draggable
    },
    maximizeWindow: function (e) {
      if (!this.maximized) {
        this.coords.left = 0
        this.coords.top = 0
      } else {
        this.coords.left = this.coords.last_left
        this.coords.top = this.coords.last_top
      }
      this.maximized = !this.maximized
      this.draggable = !this.draggable
    },
    mouseDown: function (e) {
      this.mousedown = true
      this.p.pos3 = e.clientX
      this.p.pos4 = e.clientY
    },
    mouseUp: function (e) {
      this.mousedown = false
    },
    elementDrag: function (e) {
      if (this.mousedown && this.draggable) {
        e = e || window.event
        e.preventDefault()
        // calculate the new cursor position:
        this.p.pos1 = this.p.pos3 - e.clientX
        this.p.pos2 = this.p.pos4 - e.clientY
        this.p.pos3 = e.clientX
        this.p.pos4 = e.clientY
        // set the element's new position:
        this.coords.top = (this.coords.top - this.p.pos2)
        this.coords.left = (this.coords.left - this.p.pos1)
        this.coords.last_top = this.coords.top
        this.coords.last_left = this.coords.left
      }
    }
  },
  send () {

  }
}
</script>

<style media="screen" lang="scss">

@import "./src/scss/main.scss";

$w-head-bg: $blue; // HEADER BACKGROUND COLOR
$w-head-clr: $white; // HEADER FONT COLOR
$w-body-bg: $white; // BODY BACKGROUND COLOR
$w-body-clr: $black; // BODY FONT COLOR
$w-min-bg: $green; // MIN BACKGROUND COLOR
$w-max-bg: $yellow; // MAX BACKGROUND COLOR
$w-close-bg: $red; // CLOSE BACKGROUND COLOR
$w-icons-clr: $white; // ICONS FONT COLOR

.w-min {
  .body {
    display: none !important;
  }
}
.w-max {
  width: 100vw !important;
  height: 100vh !important;
  .body {
    min-height: 100% !important;
  }
}
.window {
  width: 500px;
  max-width: 100%;
  max-height: 100vh;
  border-radius: 10px;
  overflow: hidden;
  position: absolute;

  .circle {
    width: 16px;
    height: 16px;
    border-radius: 50%;
    margin: 0 4px;
  }
  .min { background: $w-min-bg; }
  .max { background: $w-max-bg; }
  .close { background: $w-close-bg; }
  .min, .max, .close { color: $w-icons-clr; }
  .head {
    font-weight: 600;
    padding: 8px 12px;
    background: $w-head-bg;
    color: $w-head-clr;
  }

  .body {
    overflow-x: auto;
    min-height: 300px;
    background: $w-body-bg;
    color: $w-body-clr;
  }
}
</style>
