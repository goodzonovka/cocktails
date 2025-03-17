<script setup>
const props = defineProps({
  cocktail: {
    type: Object,
    required: true,
  }
})
</script>

<template>
  <div class="root">
    <RouterLink :to="`/cocktails/${cocktail.idDrink}`">
      <div class="pic" :style="`background-image: url(${cocktail.strDrinkThumb})`"></div>
    </RouterLink>
    <div class="name">{{ cocktail.strDrink }}</div>
  </div>
</template>

<style lang="sass" scoped>
.root
  width: calc((100% - 76px) / 3)

.pic
  width: 120px
  height: 120px
  margin: 0 auto 15px
  background-repeat: no-repeat
  background-position: 50% 50%
  background-size: 100%

.name
  letter-spacing: 0.1em
</style>