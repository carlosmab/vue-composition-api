<script setup> 
import { ref, computed, onMounted } from 'vue';

import BlogPost from "./components/BlogPost.vue";
import PaginationPosts from "./components/PaginationPosts.vue";
import LoadingSpinner from "./components/LoadingSpinner.vue";

const postPerPage = 10;

const posts = ref([]);
const startPost = ref(0);
const endPost = ref(postPerPage);
const favPost = ref("");
const loading = ref(true);

const changeFavorite = (post) => {
  favPost.value = post;
}

const nextPage = () => {
  startPost.value += postPerPage;
  endPost.value += postPerPage;
}

const prevPage = () => {
  startPost.value -= postPerPage;
  endPost.value -= postPerPage;
}

const nextDisabled = computed(() => {
  return startPost.value + postPerPage >= posts.value.length;  
})

const previousDisabled = computed(() => {
  return startPost.value <= 0;  
})

const fetchData = async() => {
  loading.value = true;
  try { 
    const res = await fetch('https://jsonplaceholder.typicode.com/posts');
    posts.value = await res.json();
  } catch (error) {
    console.log(error);
  } finally {
    setTimeout(()=>{
      loading.value = false;
    }, 1000);
  }
}

fetchData();

</script>

<template>
  <LoadingSpinner v-if="loading"/>
  <div v-else class="container">
    <h1>App</h1>
    <h2>My favorite post: {{ favPost }}</h2>
    <PaginationPosts 
      :nextDisabled="nextDisabled"
      :previousDisabled="previousDisabled"
      @nextPage="nextPage"
      @prevPage="prevPage"
    />
    <BlogPost 
      v-for="post in posts.slice(startPost, endPost)"
      :key="post.id"
      :title="post.title"
      :id="post.id"
      :body="post.body"
      @changeFavorite="changeFavorite"
    />
  </div>
</template>