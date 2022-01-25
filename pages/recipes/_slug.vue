<template>
  <div>
    <RecipeNav :toc="recipe.toc" />
    <div class="mt-24 px-4 py-10">
      <article class="prose prose-lg prose-stone mx-auto">
        <NuxtImg v-if="recipe.featuredImage" preload :src="recipe.featuredImage" :alt="recipe.title" class="max-h-96 w-auto" />
        <h1 class="mb-6">{{ recipe.title }}</h1>
        <div class="not-prose">
          <ul v-if="recipe.tags" class="flex space-x-4 items-center">
              <NuxtLink :to="`/tags/${tag}`" v-for="(tag, i) in recipe.tags" :key="i">
                <li class="inline-flex items-center px-2 py-1 rounded text-xs uppercase tracking-wide font-semibold"
                  :class="{ 'text-green-800 bg-green-100': tag === 'keto', 'text-pink-800 bg-pink-100': tag === 'dessert' }"
                  >
                    {{ tag }}
                </li>
              </NuxtLink>
          </ul>
        </div>
        <p>{{ recipe.description }}</p>
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
