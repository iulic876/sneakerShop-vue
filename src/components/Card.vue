<script setup>
import { inject } from "vue";

const props = defineProps({
  id: Number,
  imageUrl: String,
  title: String,
  price: Number,
  isFavorite: Boolean,
  isAdded: Boolean,
  onClickAdd: Function,
  onClickFavorite: Function,
});

const addToFavorite = inject("addToFavorite");

const onClickFavorite = () => {
  const obj = {
    ...props,
    parentId: props.id,
  };
  addToFavorite(obj);
};
</script>
<template>
  <div>
    <div
      class="relative bg-white border border-slate-100 rounded-3xl p-8 cursor-pointer hover:-translate-y-2 hover:shadow-xl transition"
    >
      <img
        :src="
          isFavorite ? './src/assets/like-2.svg' : './src/assets/like-1.svg'
        "
        alt=""
      />
      <img :src="imageUrl" alt="sneakers1" />
      <p class="mt-2">{{ title }}</p>
      <div class="flex justify-between mt-5">
        <div class="flex flex-col">
          <span class="text-slate-400">Price</span>
          <b> ${{ price }}</b>
        </div>
        <img
          :src="!isAdded ? './src/assets/plus.svg' : './src/assets/checked.svg'"
        />
      </div>
    </div>
  </div>
</template>
