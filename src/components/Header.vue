<template>
  <div>
    <header
      class="flex justify-between border-b border-slate-200 px-10 py-8 py-5"
    >
      <div class="flex items-center gap-4">
        <img src="/src/assets/logo.png" alt="logo" class="w-10" />
        <div class="flex flex-col">
          <h2 class="text-xl font-bold uppercase">Vue Sneakers</h2>
          <p class="text-slate-400">Best Shop sneakers</p>
        </div>
      </div>
      <!--right part of HEADER-->

      <ul class="flex items-center gap-10">
        <li
          class="flex items-center cursor-pointer gap-3 text-slate-500 hover:text-black"
        >
          <img src="/src/assets/cart.svg" alt="cart" />
          <span>$260</span>
        </li>
        <li
          class="flex items-center cursor-pointer gap-3 text-slate-500 hover:text-black"
        >
          <img src="/src/assets/heart.svg" alt="Favorite" />
          <span>Favorite</span>
        </li>
        <li
          class="flex items-center cursor-pointer gap-3 text-slate-500 hover:text-black"
        >
          <img src="/src/assets/profile.svg" alt="Profile" />
          <span>Profile</span>
        </li>
      </ul>
    </header>
  </div>
</template>
