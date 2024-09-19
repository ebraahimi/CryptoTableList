<script setup>
import { ref, computed } from 'vue';
import { useRouter } from 'vue-router';
import tagsData from '@/stores/tagsData.json';
let tags = ref(tagsData);
const router = useRouter();

function applyFilters() {
  const queryParams = {
    symbol: '',
    tags: '', 
    mistakes: 'Mistakes', 
    side: 'All', 
    duration: 'All' 
  };

  router.push({ name: 'filteredTable', query: queryParams });
}
</script>

<template>
  <form >
    <div class="bg-blue-900 px-4 py-2">
      <div class="container flex flex-row justify-around items-center">
        <!-- symbols -->
        <div class="flex flex-row items-center">
          <label for="symbol" class="text-sm text-white pr-2">Symbol:</label>
          <input type="text" name="symbol" id="symbol"  class="rounded-md text-gray-900 shadow-sm ring-1 ring-inset ring-gray-300 placeholder:text-gray-400 focus:ring-2 focus:ring-inset focus:ring-indigo-600 sm:text-sm sm:leading-6" placeholder="Symbol">
        </div>
        <!-- tags -->
        <div class="flex flex-row items-center pr-2">
          <label for="tags" class="text-sm text-white pr-2">Tags:</label>
          <select name="tags" id="tags" class="rounded-md py-2.5 text-gray-900 shadow-sm ring-1 ring-inset ring-gray-300 focus:ring-2 focus:ring-inset focus:ring-indigo-600 sm:max-w-xs sm:text-sm sm:leading-6 placeholder:text-gray-400" placeholder="Tags">
            <option disabled selected >Tags</option>
            <option v-for="( tag , id) in [...tags]" :key="id" name="{{tag.tags}}">{{ tag.tags }}</option>
          </select>
        </div>
        <!-- mistakes -->
        <div class="flex flex-row items-center pr-2">
          <label for="mistakes" class="text-sm text-white pr-2">Mistakes:</label>
          <select name="mistakes" id="mistakes" class="w-auto rounded-md py-2.5 text-gray-900 shadow-sm ring-1 ring-inset ring-gray-300 focus:ring-2 focus:ring-inset focus:ring-indigo-600 sm:max-w-xs sm:text-sm sm:leading-6 placeholder:text-gray-400" placeholder="Mistakes">
            <option class="disabled">Mistakes</option>
            <option>Canada</option>
            <option>Mexico</option>
          </select>
        </div>
        <!-- sides -->
        <div class="flex flex-row items-center pr-2">
          <label for="side" class="text-sm text-white pr-2">Sides:</label>
          <select name="side" id="side" class="w-auto rounded-md py-2.5 text-gray-900 shadow-sm ring-1 ring-inset ring-gray-300 focus:ring-2 focus:ring-inset focus:ring-indigo-600 sm:max-w-xs sm:text-sm sm:leading-6 placeholder:text-gray-400" placeholder="Sides">
            <option class="disabled">All</option>
            <option>Mexico</option>
          </select>
        </div>
        <!-- duration -->
        <div class="flex flex-row items-center pr-2">
          <label for="duration" class="text-sm text-white pr-2">Duration:</label>
          <select name="duration" id="duration" class="w-auto rounded-md py-2.5 text-gray-900 shadow-sm ring-1 ring-inset ring-gray-300 focus:ring-2 focus:ring-inset focus:ring-indigo-600 sm:max-w-xs sm:text-sm sm:leading-6 placeholder:text-gray-400" placeholder="Duration">
            <option class="disabled">All</option>
            <option>Mexico</option>
          </select>
        </div>
        <!-- Date range -->
        <div class="flex flex-row items-center">
          <label for="dateRange" class="text-sm text-white pr-2">From:</label>
          <input type="date" class="w-auto rounded-md  py-2.5 text-gray-900 shadow-sm ring-1 ring-inset ring-gray-300 focus:ring-2 focus:ring-inset focus:ring-indigo-600 sm:max-w-xs sm:text-sm sm:leading-6 placeholder:text-gray-400" value="Start date"/>
         <label for="dateRange" class="text-sm text-white px-2">To: </label>
          <input type="date" class="w-auto rounded-md ml-1 py-2.5 text-gray-900 shadow-sm ring-1 ring-inset ring-gray-300 focus:ring-2 focus:ring-inset focus:ring-indigo-600 sm:max-w-xs sm:text-sm sm:leading-6 placeholder:text-gray-400" value="End date"/>
        </div>
        <!-- hr line -->
        <div class="flex flex-row items-center px-3">
          <Span class="text-white text-lg">|</Span>
        </div>
        <!-- btns -->
        <div class="flex flex-row items-center justify-end gap-x-3">
            <button type="submit" class="rounded-md bg-green-500 p-3 w-auto text-sm font-semibold text-white shadow-sm hover:bg-green-400 focus-visible:outline focus-visible:outline-2 focus-visible:outline-offset-2 focus-visible:bg-green-600" 
            @submit.prevent="applyFilters">Filter</button>
            <button type="button" class="rounded-md bg-gray-500 p-3 w-auto text-sm font-semibold text-white shadow-sm hover:bg-gray-400 focus-visible:outline focus-visible:outline-2 focus-visible:outline-offset-2 focus-visible:bg-gray-500">Clear</button>
        </div>
      </div>
    </div>
  </form> 
</template>
