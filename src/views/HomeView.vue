<script setup>
import { ref, computed } from 'vue';
import { useRouter } from 'vue-router';
import NavFilter from '../components/NavFilter.vue';
import TableHeader from '../components/TableHeader.vue';
import TableBody from '../components/TableBody.vue';
import TableRowData from '@/stores/tableRowData.json';

const router = useRouter();
const queryParams = router.currentRoute.value.query;
function applyFilters() {
  
}


//date ASC / DECS 
let ascending = ref(true);
let items = ref(TableRowData);

function toggleSort() {
  ascending.value = !ascending.value;
  sortByDate();
}
function sortByDate() {
  items.value.sort((a, b) => {
      const dateA = new Date(a.date);
      const dateB = new Date(b.date);

     // Compare years
      if (dateA.getFullYear() !== dateB.getFullYear()) {
        return ascending.value ? dateB.getFullYear() - dateA.getFullYear() : dateA.getFullYear() - dateB.getFullYear();
      }
      
      // Compare months
      if (dateA.getMonth() !== dateB.getMonth()) {
        return ascending.value ? dateB.getMonth() - dateA.getMonth() : dateA.getMonth() - dateB.getMonth();
      }
      
      // Compare days
      return ascending.value ? dateB.getDate() - dateA.getDate() : dateA.getDate() - dateB.getDate();

  });
}

const sortedItems = computed(() => {
   return [...items.value] , applyFilters();
});

// pagination
const itemsPerPage = 30;

const currentPage = ref(1);

const paginatedItems = computed(() => {
  const startIndex = (currentPage.value - 1) * itemsPerPage;
  const endIndex = startIndex + itemsPerPage;
  return items.value.slice(startIndex, endIndex);
});

const totalPages = computed(() => Math.ceil(items.value.length / itemsPerPage));

function nextPage() {
  if (currentPage.value < totalPages.value) {
    currentPage.value++;
  }
}

function prevPage() {
  if (currentPage.value > 1) {
    currentPage.value--;
  }
}

</script>

<template>
  <main>
    <!-- nav filter {there is 2 filter = A. tag filter which is going to show all the tags in list | B. date with start and end date filtter} -->
    <NavFilter />
    <!-- table -->
    <table class="container table-fixed border border-collapse  border-gray-400 ">

      <!-- table title --><!-- table sort descending by DATE by defult but can sort Ascending-->
      <TableHeader @toggleSort="toggleSort"/>

      <!-- foreach data row by pinia --><!--tags number - P&L color - notes description short charecter visibility - delete action -->
      <TableBody :sortedItems="sortedItems" @applyFilters="applyFilters"/>
      
    </table>
    <!-- pagination -->
      <div class="flex justify-center mt-4">
        <button @click="prevPage" :disabled="currentPage === 1" class="px-4 py-2 bg-gray-200 text-gray-700 rounded-md">Prev </button>
        <button @click="nextPage" :disabled="currentPage === totalPages" class="px-4 py-2 bg-gray-200 text-gray-700 rounded-md">Next</button>
      </div>
  </main>
</template>
