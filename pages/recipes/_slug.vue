<template>
  <div>
    <RecipeNav :toc="recipe.toc" />
    <div class="mt-24 px-4 py-10">
      <article class="prose prose-lg prose-stone mx-auto">
        <h1>{{ recipe.title }}</h1>
        <h2>Table of Contents</h2>
        <RecipeTableOfContents :toc="recipe.toc" />
        <nuxt-content :document="recipe" />
      </article>
      <PrevAndNext :slug="recipe.slug" class="mt-32" />
    </div>
  </div>
</template>


<script lang="ts">
export default {
  async asyncData({ $content, params }) {
    const recipe = await $content('recipes', params.slug).fetch()

    return {
      recipe
    }
  },
    head() {
    return {
      title: this.recipe.title,
      meta: [
        { hid: 'description', name: 'description', content: this.recipe.description },
        // Open Graph
        { hid: 'og:title', property: 'og:title', content: this.recipe.title },
        { hid: 'og:description', property: 'og:description', content: this.recipe.description },
        // Twitter Card
        { hid: 'twitter:title', name: 'twitter:title', content: this.recipe.title },
        { hid: 'twitter:description', name: 'twitter:description', content: this.recipe.description }
      ]
    }
  }
}
</script>
