<template>
<div>
    <h2>Ingredients</h2>
    <ul>
      <li v-for="(ingredient, idx) in ingredients" :key="idx">{{ ingredient.title }}</li>
    </ul>
  </div>
</template>

<script>
export default {
  props: {
    ingredients: {
      type: Array,
      required: true,
      title: {
        type: String,
        required: true
      }
    }
  }
}
</script>
