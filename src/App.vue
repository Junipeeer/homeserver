<template>
  <div id="viewport">
    <CenterBlob type="Welcome"/>
  </div>
</template>

<script>
import CenterBlob from './components/CenterBlob.vue'

export default {
  name: 'App',
  components: {
    CenterBlob
  }
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

#app {
  font-family: "Roboto";
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

#viewport {

}
</style>
