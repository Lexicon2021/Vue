<template>
  <heading>
    <h1>Image Gallery</h1>
    <main>
      <ul id="image-gallery">
        <div class="image-1"></div>
        <div class="image-2"></div>
        <div class="image-3"></div>
        <div class="image-4"></div>
      </ul>
    </main>
  </heading>
</template>

<script>
export default {
  name: 'PageHeading',
  props: {
    msg: String
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

#image-gallery {
  list-style-type: none;
  padding: 0;
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  grid-template-rows: repeat(4, 1ft);
  gap: 0.2rem;
  height: 90vh;
}

#image-gallery h1 {
  margin-bottom: 0;
}

.image-1 {
  grid-area: 1 / 1 / 2 /2;
}

.image-2 {
  grid-area: 1 / 2 / 2 /3;
}

.image-3 {
  grid-area: 2 / 2 /3 / 3;
}

</style>
