<template>
  <div class="blob site-blob">
    <h2>{{title}}</h2>
  </div>
  
</template>

<script>
export default {
  name: 'CategoryBlob',
  props: {
    title: String,
    bgColor: String,
    textColor: String,
    angle: {
      default: 0,
      type: Number
    }
  },
  data() {
    return {
      xTranslate: 0,
      yTranslate: 0,
      xHoverTranslate: 100,
      yHoverTranslate: 100,
    };
  },
  mounted() {
    console.log(this.angle)
    this.resizeHandler()
    window.addEventListener("resize", this.resizeHandler);
  },
  unmounted() {
    window.removeEventListener("resize", this.resizeHandler);
  },
  methods: {
    resizeHandler () {
      let radian = (this.angle - 90) / 180 * Math.PI;
      let xVal = Math.min(300, 6/7 * 0.3 * window.innerWidth) * Math.cos(radian);
      let yVal = Math.min(300, 6/7 * 0.3 * window.innerWidth) * Math.sin(radian);
      this.xTranslate = xVal + "px";
      this.yTranslate = yVal + "px";
      this.xHoverTranslate = xVal * 1.25 + "px";
      this.yHoverTranslate = yVal * 1.25 + "px";
    }
  },
  computed: {
    angleStr () {
      let str;
      if (this.angle > 270 || this.angle < 90) {
        str = this.angle + "deg";
      } else {
        str = (this.angle - 180) % 180 + "deg";
      }
      return str;
    },
    rotDir () {
      let str;
      if (this.angle >= 180 && (this.angle > 270 || this.angle < 90)) {
        str = 360 + "deg";
      } else {
        str = 0 + "deg";
      }
      return str;
    }
  }
}
</script>

<style>
.site-blob {
  box-sizing: border-box;
  padding: 40px;
  background-color: v-bind(bgColor);
  border: 2px solid v-bind(bgColor);
  color: v-bind(textColor);
  display: flex;
  justify-content: center;
  align-items: center;
  transform: translate(v-bind(xTranslate),v-bind(yTranslate));
  transition: 0.7s ease;
}

.site-blob::before {
  border-radius: 0;
  content: "";
  position: absolute;
}

.site-blob::after {
  position: absolute;
  border-radius: 50%;
  content: "";
  box-shadow: 0px 0px 3px 3px v-bind(bgColor);
  filter: blur(5px);
  transition: box-shadow 0.5s ease, filter 0.5s ease;
}

.site-blob h2 {
  font-size: 3em;
  transform: rotate(v-bind(angleStr));
  transition: transform 0.3s ease, text-shadow 0.3s ease;
}

.site-blob:hover {
  transform: translate(v-bind(xHoverTranslate),v-bind(yHoverTranslate)) scale(1.5);
}

.site-blob:hover h2 {
  transform: rotate(v-bind(rotDir));
  text-shadow: 0px 0px 10px v-bind(bgColor);
  z-index: 1;
}

.site-blob:hover::before {
  transform: translate(v-bind(xTranslate),v-bind(yTranslate)) scale(2);
}

.site-blob:hover::after {
  box-shadow: 0px 0px 1px 10px v-bind(bgColor);
  filter: blur(15px);
}

</style>