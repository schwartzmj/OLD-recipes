<template>
  <div class="container mx-auto px-10 py-24">
    <Search />
    <h1 class="text-3xl">Recipes</h1>
    <ul>
      <li v-for="recipe in recipes" :key="recipe.slug">
        <NuxtLink :to="recipe.path" class="border-b border-slate-50 hover:border-b-2">{{ recipe.title }}</NuxtLink>
      </li>
    </ul>
  </div>
</template>

<script lang="ts">
export default {
  async asyncData({ $content, params }) {
    const recipes = await $content('recipes').fetch()
    return {
      recipes
    }
  }
}
</script>
