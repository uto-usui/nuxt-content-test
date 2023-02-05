<template>
  <main>
    <content-list v-slot="{ list }" :query="createPath('/bookmark')">
      <div v-for="article in list" :key="article._path">
        <h2>{{ article.title }}</h2>
        <p>{{ article.description }}</p>
      </div>
    </content-list>
    <content-list v-slot="{ list }" :query="createPath('/note')">
      <div v-for="article in list" :key="article._path">
        <h2>{{ article.title }}</h2>
        <p>{{ article.description }}</p>
      </div>
    </content-list>
    <content-list v-slot="{ list }" :query="createPath('/tips')">
      <div v-for="article in list" :key="article._path">
        <h2>{{ article.title }}</h2>
        <p>{{ article.description }}</p>
      </div>
    </content-list>
  </main>
</template>

<script setup lang="ts">
  import { QueryBuilderParams } from '@nuxt/content/dist/runtime/types'

  const createPath = (path: string): QueryBuilderParams => {
    return { path, limit: 8 }
  }
</script>
