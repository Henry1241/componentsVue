<!-- <script>
import {ref} from "vue"

export default {
  setup(){
    const counter = ref(0);

    const increment =() => {
      counter.value++
    }

    return {
      counter,
      increment,
    };
  },
};
</script> -->

<!--<script>

export default{
  data(){
    return{
      counter: 0,
    };
  },
  methods: {
    increment(){
      this.counter++
    }
  }
}
</script>-->

<script setup>
import ButtonCounter from "@/components/ButtonCounter.vue";
import BlogPost from "@/components/BlogPost.vue";
import { computed, ref, onMounted } from "vue";
import PaginatePost from "./components/PaginatePost.vue";
import LoadingSpinner from "@/components/LoadingSpinner.vue";

const posts = ref([]);
const postXpage = 10;
const start = ref(0);
const end = ref(postXpage);
const loading = ref(true);

const favorite = ref("");

const changeFavorite = (title) => {
  favorite.value = title;
};

const next = () => {
  start.value += +postXpage;
  end.value += +postXpage;
};
const back = () => {
  start.value += -postXpage;
  end.value += -postXpage;
};

//onMounted, fetch y la constante fetchData realizan la misma operacion

// onMounted(async() =>{
//    loading.value = true;
//    try {
//      const res = await(fetch("https://jsonplaceholder.typicode.com/posts"))
//      posts.value = await res.json()
//    } catch (error) {
//      console.log(error)
//    } finally {// 
//      setTimeout(() => {
//         loading.value = false
//      }, 1000)

//  fetch("https://jsonplaceholder.typicode.com/posts")
//  .then((res) => res.json())
//  .then((data) => {
//    posts.value = data;
//  })
//  .catch((e) => console.log(e))
//  .finally(() => {
//    setTimeout(() => {
//      loading.value = false;
//    }, 0);
//  });
//}})

const fetchData = async() => {
  try {
      const res = await(fetch("https://jsonplaceholder.typicode.com/posts"))
      posts.value = await res.json()
  } catch (error) {
      console.log(error)
  } finally {// 
      setTimeout(() => {
         loading.value = false
      }, 1000)
  }
};

fetchData();

const maxLength = computed(() => posts.value.length);
</script>

<template>
  <LoadingSpinner v-if="loading" />
  <div class="container" v-else>
    <h1>APP</h1>
    <h2>Mi post favorito: {{ favorite }}</h2>
    <!--<ButtonCounter></ButtonCounter>
    <button-counter></button-counter>-->

    <PaginatePost
      @next="next"
      @prev="back"
      :inicio="start"
      :fin="end"
      :maxLength="maxLength"
      class="mb-2"
    />

    <BlogPost
      v-for="post in posts.slice(start, end)"
      :key="post.id"
      :title="post.title"
      :id="post.id"
      :body="post.body"
      @changeFavoriteName="changeFavorite"
      class="mb-2"
    ></BlogPost>
  </div>
</template>
