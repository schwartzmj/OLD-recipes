<template>
  <div>
    <input v-model="query" type="search" autocomplete="off" />

    <ul v-if="recipes.length">
      <li v-for="recipe of recipes" :key="recipe.slug">
        <NuxtLink :to="recipe.path">{{ recipe.title }}</NuxtLink>
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  data () {
    return {
      query: '',
      recipes: []
    }
  },
  watch: {
    async query (query) {
      if (!query) {
        this.recipes = []
        return
      }

      this.recipes = await this.$content('recipes')
        .only(['title', 'slug'])
        .sortBy('createdAt', 'asc')
        .limit(12)
        .search(query)
        .fetch()
    }
  }
}
</script>
