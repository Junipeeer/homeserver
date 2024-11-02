<template>
  <div class="blob category-blob">
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
      default: "0",
      type: String
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
    let radian = (this.angle - 90) / 180 * Math.PI;
    this.xTranslate = 300 * Math.cos(radian) + "px";
    this.yTranslate = 300 * Math.sin(radian) + "px";
    this.xHoverTranslate = 400 * Math.cos(radian) + "px";
    this.yHoverTranslate = 400 * Math.sin(radian) + "px";
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
.category-blob {
  background-color: transparent;
  border: 1px solid v-bind(bgColor);
  color: v-bind(textColor);
  width: 350px;
  height: 350px;
  display: flex;
  justify-content: center;
  align-items: center;
  transform: translate(v-bind(xTranslate),v-bind(yTranslate));
  transition: 0.5s ease;
}

.category-blob::before {
  width: 350px;
  height: 350px;
  border-radius: 0;
  
  content: "";
  position: absolute;
}

.category-blob h2 {
  font-size: 3em;
  transform: rotate(v-bind(angleStr));
  transition: transform 0.3s ease;
}

.category-blob:hover {
  transform: translate(v-bind(xHoverTranslate),v-bind(yHoverTranslate)) scale(1.5);
}

.category-blob:hover h2 {
  transform: rotate(v-bind(rotDir));
}

.category-blob:hover::before {
  border: 1px solid red;
  width: 800px;
  height: 800px;
  transform: translate(v-bind(xHoverTranslate),v-bind(yHoverTranslate));
}
</style>