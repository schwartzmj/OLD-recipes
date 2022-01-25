<template>
  <div>
    <h1 class="text-center text-3xl capitalize">{{ slug }} Recipes</h1>
    <RecipeList class="mt-16" :recipes="recipes" />
  </div>
</template>

<script lang="ts">
export default {
  async asyncData({ $content, params }) {
    const recipes = await $content('recipes')
      .where({ tags: { $contains: params.slug } })
      .fetch()

    return {
      recipes,
      slug: params.slug,
    }
  },
  head() {
    return {
      title: this.slug,
      meta: [
        { hid: 'description', name: 'description', content: this.slug },
        // Open Graph
        { hid: 'og:title', property: 'og:title', content: this.slug },
        {
          hid: 'og:description',
          property: 'og:description',
          content: this.slug,
        },
        // Twitter Card
        { hid: 'twitter:title', name: 'twitter:title', content: this.slug },
        {
          hid: 'twitter:description',
          name: 'twitter:description',
          content: this.slug,
        },
      ],
    }
  },
}
</script>
