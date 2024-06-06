<script setup lang="ts">
import { ref } from 'vue'
import type { RecommendStatus } from '../types'

  interface Dish {
    name?: string,
    dient?: Diet,
    status?: RecommendStatus
  }

  const restaurantStatusList = [
    "Want to Try",
    "Recommended",
    "Do Not Recommend",
    "Must Try"
  ] as const

  type Diet = 
      'vegetarian' 
    | 'vegan' 
    | 'gluten-free' ;  


  const dishList = ref<Dish[]>([])
  const newDish = ref<Dish>({
    status: 'Want to Try'
  })

  const statusList = [
    "Want to Try",
    "Recommended",
    "Do Not Recommend",
    "Must Try"
  ]
  
  function addDish() {
    dishList.value.push(
      {
        name: newDish.value.name,
        status: newDish.value.status
      }
    )
  }
</script>

<template>
  <main>
    <pre>{{ newDish }}</pre>
    <form @submit.prevent="addDish">
      <div>
        <label for="dish-name">Dish Name</label>
        <input id="dish-name" v-model="newDish.name" type="text"/>
      </div>

      <div>
        <label for="dish-status">Dish Status</label>
        <select 
          name="dish-status" 
          id="dish-status" 
          v-model="newDish.status">
            <option 
              v-for="status in statusList" 
              :value="status"
              :key="status">
                {{ status }}
            </option>
        </select>
      </div>
      <button type="submit">Add Dish</button>
    </form>

    <ul>
      <li v-for="dish in dishList" :key="dish.name">
        {{ dish.name }}
      </li>
    </ul>
  </main>
</template>
