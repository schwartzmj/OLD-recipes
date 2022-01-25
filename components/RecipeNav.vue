<template>
  <div class="hidden md:block">
    <ul class="fixed top-0 right-0 p-4 h-full w-32 flex flex-wrap flex-col divide-y-2 divide-stone-300 z-50 bg-stone-200/60 text-stone-600">
      <li
        v-for="link of tocLinks"
        :key="link.id"
        class="w-full p-1 text-base"
      >
        <NuxtLink :to="`#${link.id}`" :id="`${link.id}-nav`">{{ link.text }}</NuxtLink>
        <ul>
          <li
            v-for="child of link.children"
            :key="child.id"
            class="p-1 text-xs"
          >
            <NuxtLink :to="`#${child.id}`" :id="`${child.id}-nav`">{{ child.text }}</NuxtLink>
          </li>
        </ul>
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  props: {
    toc: {
      type: Array,
      required: true
    }
  },
  computed: {
    tocLinks() {
      // Loop over ToC links. If link has depth of 2, start a new 'ToC parent' (h2 tag). If next link has depth of 3, add it to that parent's children array. If next link has depth of 2, start a new 'ToC parent'. If next link has depth of 3, add it to that parent's children array (and so on).
      // In other words, it is an array of "h2" tags with their children "h3" tags.
      const tocLinks = []
      let currentTocParent = { children: [] }
      this.toc.forEach(link => {
        if (link.depth === 2) {
          if (currentTocParent.children.length > 0 || 'id' in currentTocParent) { // previous link was an h2 tag OR we already have an h2 tag so we should start a new one (previous one had no children)
            tocLinks.push(currentTocParent)
          }
          currentTocParent = { ...link, children: [] }
        } else {
          currentTocParent.children.push(link)
        }
      })
      tocLinks.push(currentTocParent) // push final TocParent
      return tocLinks
    }
  },
  mounted() {
    console.log(this.toc)
    this.toc.forEach(link => {
      // TODO: Get more accurate scroll spy based on height of anchor's content?
      // Maybe: https://github.com/janpaepke/ScrollMagic/issues/500#issuecomment-216463444
      const scene = this.$scrollmagic.scene({triggerElement: `#${link.id}`, duration: 500})
        .setClassToggle(`#${link.id}-nav`, 'bg-stone-300')
      this.$scrollmagic.addScene(scene)
    })
  }
}
</script>
