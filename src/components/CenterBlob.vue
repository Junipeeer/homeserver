<template>
  <div class="blob-container">
    <CategoryBlob v-for="(blob, index) in Object.values(categoryBlobs)" :key="index" @click="this.emitClick(blob.bg_color)" :title="blob.title" :bgColor="blob.bg_color" :textColor="blob.text_color" :angle="(index+1) * 360/blobCount" />
    <div class="blob center-blob">
      <h1>{{ type }}</h1>
    </div>
  </div>
</template>

<script>
import CategoryBlob from './CategoryBlob.vue'

export default {
  name: 'CenterBlob',
  components: {
    CategoryBlob
  },
  props: {
    type: String,
    categoryBlobs: Object
  },
  mounted () {
    this.blobCount = Object.keys(this.categoryBlobs).length
    for (let blob in Object.values(this.categoryBlobs)) {
      console.log(blob)
      console.log(Object.values(this.categoryBlobs))
    }
  },
  methods: {
    emitClick(input) {
      console.log(this.categoryBlobs)
      this.$emit('clicked', input)
    },
    recalcCircles (target) {
      return target;
    }
  },
  computed: {
    blobCount() {
      return Object.keys(this.categoryBlobs).length;
    }
  }
}
</script>

<style>
.blob {
  position: absolute;
  border-radius: 50%;
  display: flex;
  justify-content: center;
  align-items: center;
  width: 40vw; aspect-ratio: 1/1;
  max-width: 350px;
  min-width: 100px;
}

.blob::before, .blob::after {
  width: 40vw; aspect-ratio: 1/1;
  max-width: 350px;
}

.center-blob::after {
  position: absolute;
  border-radius: 50%;
  content: "";
  box-shadow: 0px 0px 3px 3px #f3f6f3;
  filter: blur(5px); 
}

.center-blob {
  box-sizing: border-box;
  background-color: #F6F4F3;
  border: 2px solid #F6F4F3;
  color: #212121;
  z-index: 5;
}

.center-blob h1 {
  font-size: 4.5em;
}

.blob-container {
  height: 800px;
  width: 800px;
  max-height: 80%;
  max-width: 80%;
  display: flex;
  justify-content: center;
  align-items: center;
}

.blob-container.category-blob:hover * {
  background-color: red;
}
</style>