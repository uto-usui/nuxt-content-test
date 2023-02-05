<template>
  <main>
    <content-list v-slot="{ list }" :path="path">
      <div v-for="article in list" :key="article._path">
        <nuxt-link :to="article._path">
          <h2>{{ article.title }}</h2>
          <p>{{ article.description }}</p>
        </nuxt-link>
      </div>
    </content-list>
  </main>
</template>

<script setup lang="ts">
  const { path } = useRoute()
</script>
