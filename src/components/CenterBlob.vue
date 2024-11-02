<template>
  <div class="blob">
    <h1>{{ type }}</h1>
  </div>
</template>

<script>
export default {
  name: 'CenterBlob',
  props: {
    type: String
  }
}
</script>

<style scoped>
.blob {
  border-radius: 50%;
  background-color: #294724;
  color: aliceblue;
  width: 200px;
  height: 200px;
  display: flex;
  justify-content: center;
  align-items: center;
}
</style>