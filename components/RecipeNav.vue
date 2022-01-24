<template>
  <ul class="fixed top-0 right-0 p-4 w-full flex flex-wrap items-center space-x-3 z-50 bg-stone-200 text-stone-600">
    <li
      v-for="link of toc"
      :key="link.id"
      :id="link.id + '-nav'"
      class="p-1"
      :class="{ '': link.depth === 2, 'text-sm': link.depth === 3 }"
    >
      <NuxtLink :to="`#${link.id}`">{{ link.text }}</NuxtLink>
    </li>
  </ul>
</template>

<script>
export default {
  props: {
    toc: {
      type: Array,
      required: true
    }
  },
  mounted() {
    this.toc.forEach(link => {
      const scene = this.$scrollmagic.scene({triggerElement: `#${link.id}`, duration: 500})
        .setClassToggle(`#${link.id}-nav`, 'bg-cyan-50')
      this.$scrollmagic.addScene(scene)
    })
    // // build scenes
    // this.$scrollmagic.scene({triggerElement: "#sec1"})
    //         .setClassToggle("#high1", "active") // add class toggle
    //         .addIndicators() // add indicators (requires plugin)
    //         .addTo(controller);
    // this.$scrollmagic.scene({triggerElement: "#sec2"})
    //         .setClassToggle("#high2", "active") // add class toggle
    //         .addIndicators() // add indicators (requires plugin)
    //         .addTo(controller);
    // this.$scrollmagic.scene({triggerElement: "#sec3"})
    //         .setClassToggle("#high3", "active") // add class toggle
    //         .addIndicators() // add indicators (requires plugin)
    //         .addTo(controller);
    // this.$scrollmagic.scene({triggerElement: "#sec4"})
    //         .setClassToggle("#high4", "active") // add class toggle
    //         .addIndicators() // add indicators (requires plugin)
    //         .addTo(controller);
  }
}
</script>
