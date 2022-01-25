<template>
  <div class="container mx-auto px-10 py-24">
    <Search />
    <h1 class="text-3xl">Recipes</h1>
    <RecipeList :recipes="recipes" />
  </div>
</template>

<script lang="ts">
export default {
  async asyncData({ $content, params }) {
    const recipes = await $content('recipes').fetch()
    return {
      recipes,
    }
  },
}
</script>
