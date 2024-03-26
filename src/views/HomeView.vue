<script setup>
import NavBar from "@/components/NavBar.vue";
import SideBar from "@/components/SideBar.vue";
</script>
<style>
:root {
  --background: #eff4f8;
}
</style>
<template>
  <main style="display: flex; background-color: var(--background)">
    <SideBar />
    <NavBar />
  </main>
</template>
