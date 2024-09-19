<script setup>
import { defineProps, ref } from 'vue';
import { useRoute } from 'vue-router';
import { FontAwesomeIcon } from '@fortawesome/vue-fontawesome';
import { faTrashCan } from '@fortawesome/free-regular-svg-icons';
import TableRowData from '@/stores/tableRowData.json';

const props = defineProps({
  sortedItems: Array,
});

function profitClass(value) {
    const numberValue = parseFloat(value.replace(/\$|,/g, ''));
    return numberValue >= 0 ? 'text-green-500' : 'text-red-500';
};

const filteredItems = ref([]);
const route = useRoute();

const symbol = route.query.symbol;
const tags = route.query.tags;
const mistakes = route.query.mistakes;
const side = route.query.side;
const duration = route.query.duration;

filteredItems.value = TableRowData.filter(item => {
  return item.tags.includes(tags);
});


</script>
<template>
    <tbody class="divide-y divide-gray-400">
        <tr v-for="(item, id) in sortedItems" :key="id">
            <td class="px-6 py-4 whitespace-nowrap text-center">{{ item.date }}</td>
            <td class="px-6 py-4 whitespace-nowrap text-center">{{ item.time }}</td>
            <td class="px-6 py-4 whitespace-nowrap text-center" :class="profitClass(item.PL)">{{ item.PL }}</td>
            <td class="px-6 py-4 whitespace-nowrap text-center">
                <span  class="text-xs font-medium me-2 px-2.5 py-0.5 rounded dark:bg-blue-900 dark:text-blue-100" v-for="(tag, tagIndex) in item.tags.slice(0, 2)" :key="tagIndex">{{ tag.text }}</span>
                <span class="bg-blue-100 text-blue-800 text-xs font-medium me-2 px-2.5 py-0.5 rounded dark:bg-blue-900 dark:text-blue-100" v-if="item.tags.length > 2" >+{{ item.tags.length - 2 }}</span>
            </td>
            <td  class="px-6 py-4 whitespace-nowrap text-center ">{{ item.notes.slice(0, 20) + "..." }}</td>
            <td  class="px-6 py-4 whitespace-nowrap text-center ">
                <button class="font-medium text-blue-900 dark:text-blue-900 hover:underline" @click="delete(item.id)">
                    <FontAwesomeIcon :icon="faTrashCan" />
                </button>
            </td>
        </tr>
      </tbody>
</template>

