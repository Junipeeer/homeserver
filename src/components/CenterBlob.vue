<template>
  <div class="blob-container">
    <CategoryBlob @click="this.emitClick('#F3A712')" title="Reading" bgColor="#F3A712" textColor="#F6F4F3" angle="72"/>
    <CategoryBlob @click="this.emitClick('#26BD5B')" title="Smart Home" bgColor="#26BD5B" textColor="#F6F4F3" angle="144"/>
    <CategoryBlob @click="this.emitClick('#2589BD')" title="Tools" bgColor="#2589BD" textColor="#F6F4F3" angle="216"/>
    <CategoryBlob @click="this.emitClick('#C64191')" title="_Server" bgColor="#C64191" textColor="#F6F4F3" angle="288"/>
    <CategoryBlob @click="this.emitClick('#C03221')" title="Media" bgColor="#C03221" textColor="#F6F4F3" angle="360"/>
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
    categoryBlobs: JSON
  },
  methods: {
    emitClick(input) {
      this.$emit('clicked', input)
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
  width: 30vw; aspect-ratio: 1/1;
  max-width: 350px;
  min-width: 100px;
}

.blob::before, .blob::after {
  width: 30vw; aspect-ratio: 1/1;
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
  font-size: 5em;
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