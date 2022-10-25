<script setup>
// const props = defineProps(["title", "id", "description"]);
defineProps({
  title: String,
  id: Number,
  body: {
    type: String,
    default: "Without description"
  }
})
const emit = defineEmits(["changeFavorite"])

</script>

<template>
  <div class="card mb-2">
    <div class="card-body">
      <div class="card-title">{{ id }} - {{ title }}</div>
      <p>{{ body }}</p>
      <button 
        class="btn btn-outline-primary"
        @click="emit('changeFavorite', title)"
      >Fav</button>
    </div>
  </div>
</template>
