<template>
  <main>
    <content-list v-slot="{ list }" :path="'/bookmark'">
      <div v-for="article in list" :key="article._path">
        <h2>{{ article.title }}</h2>
        <p>{{ article.description }}</p>
      </div>
    </content-list>
  </main>
</template>

<script setup lang="ts"></script>
