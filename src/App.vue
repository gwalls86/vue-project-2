<script setup>  
  import {ref, onMounted} from 'vue';
    
  import BlogPost from './components/BlogPost.vue';  
  import PaginatePost from './components/PaginatePost.vue';
  import LoadingSpinner from './components/LoadingSpinner.vue';

  const posts = ref([]);
  const postXpag = 10;
  const inicio = ref(0);
  const fin = ref(postXpag);
  const loading = ref(true);


  const next = () => {
    inicio.value += postXpag; 
    fin.value += postXpag; 
  }

  const prev = () => {
    inicio.value += - postXpag; 
    fin.value += - postXpag; 
  }

  const favorito = ref('');

  const cambiarFavorito = (id) => {
    favorito.value = id;    
  }
 
  /* Opcion 1 con onMounted */
  // onMounted(async() => {  
  //    try{
  //     const res = await fetch("http://jsonplaceholder.typicode.com/posts");
  //     posts.value = await res.json();
  //   } catch(error) {
  //     console.log(error);
  //   } finally {
  //     loading.value = false;
  //   }
  // });

  /* Opcion 2 con .then */
  //fetch('http://jsonplaceholder.typicode.com/posts')
  //.then(res => res.json())
  //.then(data => {posts.value = data})
  //.catch((e) => { console.log(e) })
  //.finally(() => loading.value = false);

  /* Mejor Opcion 3 -> Usando async sin onMounted*/
  const fetchData = async() => {
    try{
      const res = await fetch("https://jsonplaceholder.typicode.com/posts");
      posts.value = await res.json();
    } catch(error) {
      console.log(error);
    } finally {
      loading.value = false;
    }
  }

  fetchData();
  

</script>

<template>
  <LoadingSpinner v-if="loading"></LoadingSpinner>
  <div class="container" v-else>
    <h1>APP</h1>
    <h2>Mi Post Favorito: {{ favorito }}</h2>

    <PaginatePost 
      @nextname = "next"
      @prevname = "prev"
      :inicioname = "inicio"
      :finname = "fin"
      :maxlengthname="posts.length"
      class="mb-2"
    >
    </PaginatePost>


    <BlogPost
      v-for="post in posts.slice(inicio,fin)"
      :key="posts.id"
      :title=post.title
      :body=post.body
      :id="post.id"
      @cambiarFavoritoNombre="cambiarFavorito"
      class="mb-2">
    </BlogPost> 

  </div>
</template>

<style scoped>

</style>
