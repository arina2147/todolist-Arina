<!-- src/App.vue -->
<script setup lang="ts">
import ClickCounter from './components/ClickCounter.vue'
import ItemList from './components/ItemList.vue'
import WelcomeMessage from './components/WelcomeMessage.vue'
</script>

<template>
  <main>
    <WelcomeMessage msg="講習会の課題" />
    <ClickCounter />
    <ItemList />
  </main>
</template>

<style scoped>
main {
  padding: 2rem;
}
</style>
