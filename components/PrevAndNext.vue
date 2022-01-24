<template>
  <div class="max-w-lg mx-auto flex items-center justify-between space-x-2">
    <div v-if="prev" class="text-center">
      <NuxtLink :to="prev.path" class="flex items-center justify-center p-2 from-stone-400 to-stone-600 bg-gradient-to-l shadow-lg shadow-stone-400 hover:bg-gradient-to-bl text-stone-50">
        <svg xmlns="http://www.w3.org/2000/svg" class="h-5 w-5" fill="none" viewBox="0 0 24 24" stroke="currentColor">
          <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M10 19l-7-7m0 0l7-7m-7 7h18" />
        </svg>
        <span class="ml-2">Previous</span>
      </NuxtLink>
      <p class="mt-3 text-sm text-stone-600">{{ prev.title }}</p>
    </div>

    <div v-if="next" class="text-center">
      <NuxtLink :to="next.path" class="flex items-center justify-center p-2 from-stone-400 to-stone-600 bg-gradient-to-r shadow-lg shadow-stone-400 hover:bg-gradient-to-br text-stone-50">
        <span class="ml-2">Next</span>
        <svg xmlns="http://www.w3.org/2000/svg" class="ml-2 h-5 w-5" fill="none" viewBox="0 0 24 24" stroke="currentColor">
          <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M14 5l7 7m0 0l-7 7m7-7H3" />
        </svg>
      </NuxtLink>
      <p class="mt-3 text-sm text-stone-600">{{ next.title }}</p>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    slug: {
      type: String,
      required: true
    }
  },
  data: () => ({
    prev: null,
    next: null
  }),
  async fetch() {
    const [prev, next] = await this.$content('recipes')
      .only(['title', 'path'])
      .sortBy('date')
      .surround(this.slug)
      .fetch()
      this.prev = prev
      this.next = next
  },
  // fetchOnServer: false,
  // multiple components can return the same `fetchKey` and Nuxt will track them both separately
  fetchKey: 'prev-and-next-' + Date.now(),
  // alternatively, for more control, a function can be passed with access to the component instance
  // It will be called in `created` and must not depend on fetched data
  // fetchKey(getCounter) {
  //   // getCounter is a method that can be called to get the next number in a sequence
  //   // as part of generating a unique fetchKey.
  //   return this.someOtherData + getCounter('sidebar')
  // }
}
</script>
