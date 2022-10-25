<script setup>
defineProps(["previousDisabled", "nextDisabled"]);
const emit = defineEmits(["nextPage", "prevPage"]);

const prevPage = () => emit("prevPage");
const nextPage = () => emit("nextPage");

</script>

<template>
  <div class="btn-group mb-2" role="group" aria-label="Basic example">
    <button 
      type="button" 
      class="btn btn-outline-primary" 
      :disabled="previousDisabled"
      @click="prevPage"
    >
      Previous
    </button>
    <button 
      type="button" 
      class="btn btn-outline-primary" 
      :disabled="nextDisabled"
      @click="nextPage"
    >
      Next
    </button>
  </div>
</template>

