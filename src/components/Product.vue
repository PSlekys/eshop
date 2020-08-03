<template>
  <div class="card">
    <div class="card-image">
      <figure class="image is-4by3">
        <img :src="image" :alt="name" />
      </figure>
    </div>
    <div class="card-content">
      <div class="media">
        <div class="media-content">
          <p class="title is-4">{{ name }}</p>
          <p class="subtitle is-6">{{ price }} Eur</p>
        </div>
      </div>

      <div class="content">
        {{ description }}
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "Product",
  props: { image: String, name: String, description: String, price: Number },
};
</script>

<style scoped>
img {
  object-fit: contain;
}
</style>
