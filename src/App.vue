<template>
  <div id="transition-circle" class="transition" @click="removeTransition"></div>
  <main id="viewport">
    <CenterBlob @clicked="addTransition" type="Welcome" :categoryBlobs="this.blobs.category_blobs"/>
  </main>
</template>

<script>
import CenterBlob from './components/CenterBlob.vue'
import blobs from './assets/blobs.json'

export default {
  name: 'App',
  components: {
    CenterBlob
  },
  data() {
    return {
      mousePosX: 0,
      mousePosY: 0,
      mouseXPx: "0px",
      mouseYPx: "0px",
      viewportPosX: "-100%",
      viewportPosY: "-100%",
      transitionBGColor: "#fff",
      blobs: blobs
    };
  },
  mounted() {
    let change = 0;
    document.addEventListener("mousemove", (event) => {
      this.mousePosX = event.clientX;
      this.mousePosY = event.clientY;
      if (change % 3 == 0) { // only ajust the viewport every three times to save on lag
        this.changeViewport();
        change = 1
      } else {
        change++
      }
    });

    const viewport = document.getElementById("viewport");
    const dotSize = 1; // Size of the main dot
    const spacing = 50; // Distance between dots

    const width = viewport.clientWidth;
    const height = viewport.clientHeight;
    const canvas = document.createElement('canvas');
    canvas.width = width;
    canvas.height = height;
    const context = canvas.getContext('2d');

    context.fillStyle = '#F6F4F3'; // Set color for main dots

    for (let x = 0; x < width; x += spacing) {
      for (let y = 0; y < height; y += spacing) {
        // Draw main dot with shadow effect
        context.shadowColor = 'rgba(96, 165, 136, 0.5)'; // Light color for shadow with transparency
        context.shadowBlur = 2; // Blur radius for shadow

        context.beginPath();
        context.arc(x, y, dotSize, 0, Math.PI * 2);
        context.fill();

        // Reset shadow properties
        context.shadowColor = 'transparent';
        context.shadowBlur = 0;
      }
    }

    viewport.style.backgroundImage = `url(${canvas.toDataURL()})`;
  },
  methods: {
    changeViewport() {
      let xScale = (this.mousePosX / (window.innerWidth / 2) - 1) * 1000/window.innerWidth;
      let yScale = (this.mousePosY / (window.innerHeight / 2) - 1) * 1000/window.innerHeight;

      this.viewportPosX = -100 + -60 * xScale + "%";
      this.viewportPosY = -100 + -60 * yScale + "%";
    },
    addTransition(input) {
      this.mouseXPx = this.mousePosX + "px";
      this.mouseYPx = this.mousePosY + "px";
      this.transitionBGColor = input;
      let elem = document.getElementById("transition-circle");
      elem.classList.add("trans-active");
    },
    removeTransition() {
      this.mouseXPx = this.mousePosX + "px";
      this.mouseYPx = this.mousePosY + "px";
      let elem = document.getElementById("transition-circle");
      elem.classList.remove("trans-active");
    }
  },
}
</script>

<style>

@font-face {
  font-family: "Roboto";
  src: url(./assets/fonts/roboto/Roboto-Regular.ttf);
  font-weight: normal;
  font-style: normal;
}

@font-face {
  font-family: "Roboto";
  src: url(./assets/fonts/roboto/Roboto-Bold.ttf);
  font-weight: bold;
  font-style: normal;
}

@font-face {
  font-family: "Roboto";
  src: url(./assets/fonts/roboto/Roboto-Italic.ttf);
  font-weight: normal;
  font-style: italic;
}

@font-face {
  font-family: "Roboto";
  src: url(./assets/fonts/roboto/Roboto-BoldItalic.ttf);
  font-weight: bold;
  font-style: italic;
}

body,html {
  margin: 0;
  padding: 0;
  
}

#app {
  position: absolute;
  top: 0;
  bottom: 0;
  left: 0;
  right: 0;
  font-family: "Roboto";
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #f3f6f3;
  height: 100%;
  width: 100%;
  overflow: hidden;
}

#viewport {
  position: absolute;
  background-color: rgb(37, 37, 37);
  top: v-bind(viewportPosY);
  left: v-bind(viewportPosX);
  width: 300%;
  height: 300%;
  display: flex;
  justify-content: center;
  align-items: center;
  transition: top 0.05s linear, left 0.05s linear;
}

.transition {
  position: absolute;
  border-radius: 50%;
  transform: translate(-50px, -50px) scale(0);
  left: v-bind(mouseXPx);
  top: v-bind(mouseYPx);
  width: 100px;
  height: 100px;
  z-index: 10;
  background-color: v-bind(transitionBGColor);
  transition: transform 0.5s ease;
}

.trans-active {
  transition: transform 1s ease;
  transform: translate(-50px, -50px) scale(50);
}
</style>
