<script setup>
import AppLayout from '../components/AppLayout.vue'
import CocktailThumb from '@/components/CocktailThumb.vue'
import {useRootStore} from '@/stores/root'
import {storeToRefs} from 'pinia'
import bgImage from '@/assets/img/bg-1.jpg'

const rootStore = useRootStore()
rootStore.getIngredients()

const {ingredients, ingredient, cocktails} = storeToRefs(rootStore)

function getCocktails() {
  rootStore.getCocktails(rootStore.ingredient)
}

function removeIngredient() {
  rootStore.setIngredient(null)
}
</script>

<template>
  <AppLayout
      :imgUrl="bgImage"
             :backFunc="removeIngredient"
             :is-back-button-visible="!!ingredient"
  >
    <div class="wrapper">
      <div v-if="!ingredient || !cocktails" class="info">
        <div class="title">Choose your drink</div>
        <div class="line"></div>

        <div class="select-wrapper">
          <el-select
              v-model="rootStore.ingredient"
              placeholder="Choose main ingredient"
              filterable
              allow-create
              size="large"
              class="select"
              @change="getCocktails"
          >
            <el-option
                v-for="item in ingredients"
                :key="item.strIngredient1"
                :label="item.strIngredient1"
                :value="item.strIngredient1"
            />
          </el-select>
        </div>
        <div class="text">
          Try our delicious cocktail recipes for every occasion. Find delicious cocktail recipes by ingredient through
          our cocktail generator.
        </div>
        <img src="/src/assets/img/cocktails.png" width="345" alt="Cocktails" class="img">
      </div>

      <div v-else class="info">
        <div class="title">COCKTAILS WITH {{ ingredient }}</div>
        <div class="line"></div>
        <div class="cocktails">
          <CocktailThumb v-for="cocktail in cocktails" :key="cocktail.idDrink" :cocktail="cocktail"/>
        </div>
      </div>
    </div>
  </AppLayout>
</template>

<style lang="sass" scoped>
@use "@/assets/styles/variables" as *

.select-wrapper
  padding-top: 50px

.select
  width: 220px

.text
  width: 516px
  max-width: 100%
  margin: 0 auto
  padding-top: 50px
  line-height: 36px
  letter-spacing: 0.1em
  color: $textMuted

.img
  margin-top: 60px

.cocktails
  width: 600px
  max-height: 400px
  overflow-y: auto
  display: flex
  justify-content: center
  flex-wrap: wrap
  margin-top: 60px
  column-gap: 38px
  row-gap: 41px
</style>