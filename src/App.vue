<script setup>
import { onMounted, reactive, ref, watch, provide } from "vue";
import axios from "axios";
import Header from "./components/Header.vue";
import CardList from "./components/CardList.vue";
import Drawer from "./components/Drawer.vue";

const items = ref([]);

const filters = reactive({
  sortBy: "",
  searchQuery: "",
});

const fetchFavorites = async () => {
  try {
    const { data: favorites } = await axios.get(
      "https://65daa976007c08e1.mokky.dev/favorites"
    );
    console.log("Favorites:", favorites);
    items.value = items.value.map((item) => {
      const favorite = favorites.find((fav) => fav.parent?.id === item.id);
      if (!favorite) {
        return item;
      }
      return {
        ...item,
        isFavorite: true,
        favoriteID: favorite.id,
      };
    });
  } catch (error) {
    console.error(error);
  }
};

const fetchItems = async () => {
  try {
    const { data } = await axios.get(
      "https://65daa976007c08e1.mokky.dev/items"
    );
    items.value = data.map((obj) => ({
      ...obj,
      isFavorite: false,
      isAdded: false,
    }));
    console.log("Items:", data);
  } catch (error) {
    console.error(error);
  }
};

const onChangeSelect = (event) => {
  filters.sortBy = event.target.value;
};

watch(filters, async () => {
  try {
    const { data } = await axios.get(
      `https://65daa976007c08e1.mokky.dev/items?sortBy=${encodeURIComponent(
        filters.sortBy
      )}`
    );
    items.value = data;
  } catch (error) {
    console.error(error);
  }
});

const addToFavorite = (item) => {
  item.isFavorite = true;
  console.log("Added to Favorites:", item);
};

onMounted(async () => {
  await fetchItems();
  await fetchFavorites();
});

provide("addToFavorite", addToFavorite);
</script>

<template>
  <div class="w-4/5 m-auto bg-white rounded-xl shadow-xl py-20">
    <!-- HEADER -->
    <Header />

    <!-- FILTERS & SEARCH -->
    <div class="flex justify-between items-center px-10">
      <h2 class="text-3xl font-bold mb-8">All sneakers</h2>
      <div class="flex gap-4">
        <!-- Dropdown for Sorting -->
        <select
          @change="onChangeSelect"
          class="py-2 px-3 border rounded-md outline-none focus:ring-2 focus:ring-gray-400"
        >
          <option value="name">Sort by Name</option>
          <option value="-price">Price Descending</option>
          <option value="price">Price Ascending</option>
        </select>

        <!-- Search Input -->
        <div class="relative">
          <img
            src="/src/assets/search.svg"
            alt="Search Icon"
            class="absolute left-4 top-1/2 transform -translate-y-1/2 w-5 h-5"
          />
          <input
            type="text"
            placeholder="Search..."
            v-model="filters.searchQuery"
            class="border rounded-md py-2 pl-12 pr-4 outline-none focus:border-gray-400"
          />
        </div>
      </div>
    </div>

    <!-- CARD LIST -->
    <div class="mt-10 px-10">
      <CardList :items="items" />
    </div>
  </div>
</template>
