<template>
  <div class="container mx-auto">
    <ul class="flex flex-wrap justify-center gap-4">
      <li v-for="(recipe, i) in recipes" :key="i" class="transition-all duration-300 ease-in-out" :class="{
        'hover:rotate-1': i % 2 === 0,
        'hover:-rotate-1': i % 2 != 0
      }">
        <NuxtLink :to="`/recipes/${recipe.slug}`" class="group block relative">
          <NuxtImg class="relative" width="300" height="300" fit="cover" :src="recipe.featuredImage || '/images/recipes/featured-image-placeholder.jpg'" :alt="recipe.title" />
          <h3 class="mt-2 text-xl text-center">{{ recipe.title }}</h3>
          <!-- Hover overlay -->
          <div class="opacity-0 group-hover:opacity-100 absolute top-0 left-0 w-[300px] h-[300px] bg-stone-200/50 transition-all duration-1000">
            <ul v-if="recipe.tags" class="flex flex-col items-end space-y-1">
              <li
                v-for="(tag, i) in recipe.tags"
                :key="i"
                class="inline-flex items-center px-2 py-1 rounded text-xs uppercase tracking-wide font-semibold"
                :class="{
                  'text-green-800 bg-green-100': tag === 'keto',
                  'text-pink-800 bg-pink-100': tag === 'dessert',
                  'text-cyan-800 bg-cyan-100': tag === 'fathead',
                }"
              >
                {{ tag }}
              </li>
            </ul>
          </div>
        </NuxtLink>
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  props: {
    recipes: {
      type: Array,
      required: true,
      title: {
        type: String,
        required: true
      },
      slug: {
        type: String,
        required: true
      },
      featuredImage: {
        type: String,
        required: false
      },
      tags: {
        type: Array,
        required: false
      }
    },
  },
}
</script>
