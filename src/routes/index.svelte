<script context="module">
   let key ='7f420f598193023be29b498f58af9748';
   export async function load({fetch}){
      const res = await fetch(`https://api.themoviedb.org/3/movie/popular?api_key=${key}&language=en-US&page=1`);
      const data = await res.json();
      if(res.ok){
         return{
            props: {popular: data.results}
         }
      }
   };
</script>

<script>
   import PopularMovies from "../components/PopularMovies.svelte";
   import "../../src/global.css";
   import SearchMovies from "../components/SearchMovies.svelte";
   import {fly} from "svelte/transition";
   export let popular;
</script>

<section in:fly={{y: 100, duration: 500}} out:fly={{y: 0, duration: 500}}>
   <SearchMovies />
   <PopularMovies movies ={popular}/>
</section>