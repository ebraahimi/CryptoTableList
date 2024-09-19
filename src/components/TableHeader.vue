<script setup>
import { defineEmits } from 'vue';

const emit = defineEmits(['toggleSort']);

function toggleSort() {
    emit('toggleSort');
}


</script>
<template>
    <thead >
        <tr class="bg-blue-200 container">
            <th class="w-2" @click="toggleSort">Date</th>
            <th class="w-2">Time</th>
            <th class="w-1">P&L</th>
            <th class="w-3">Tags</th>
            <th class="w-3">Notes</th>
            <th class="w-1">Action</th>
        </tr>
    </thead>
</template>