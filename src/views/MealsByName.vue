<template>
    <div class="p-8">
        <input 
            type="text"
            v-model="keyword" 
            class="rounded border-2 border-gray-200 w-full"
            placeholder="Search for Meals"
            @change="searchMeals"
        >
    </div>

    <div class="grid grid-cols-1 md:grid-cols-3 gap-5 p-8">
        <div v-for="meal of meals" :key="meal.idMeal" class="bg-white shadow rounded-xl">
            <div class="p-3">
                <img :src="meal.strMealThumb" :alt="strMeal" class="rounded-t-xl h-48 w-full object-cover">
                    <h3 class="p-3 font-bold">{{ meal.strMeal }}</h3>
                    <p>{{ meal.strInstructions.substring(0,100) }}</p>
                <div class="pt-3 flex items-center justify-between">
                    <a :href="meal.strYoutube" target="_blank" 
                    class="px-3 py-2 rounded border-2 border-red-600 bg-red-500 text-white hover:bg-red-600 hover:text-white transition-colors">
                        YouTube
                    </a>
                </div>
            </div>
        </div>
    </div>
</template>

<script setup>
import { computed } from '@vue/reactivity'
import { ref } from 'vue';
import store from '../store';

const keyword = ref('');
const meals = computed(() => store.state.searchedMeals)

function searchMeals() {
    store.dispatch('searchMeals', keyword.value)
}

</script>