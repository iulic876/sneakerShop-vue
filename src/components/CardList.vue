<script setup>
import Card from "./Card.vue";

defineProps({
  items: Array,
});
</script>
<template>
  <div class="p-10">
    <div class="grid grid-cols-4 gap-5">
      <Card
        v-for="item in items"
        :id="item.id"
        :key="item.id"
        :title="item.title"
        :image-url="item.imageUrl"
        :price="item.price"
        :isAdded="false"
        :is-favorite="false"
        :onClickAdd="onClickAdd"
        :isFavorite="item.isFavorite"
      />
    </div>
  </div>
</template>
