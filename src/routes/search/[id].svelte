<script context="module">

	let key = '7f420f598193023be29b498f58af9748';
	export async function load({ fetch, params }) {
		const res = await fetch(`https://api.themoviedb.org/3/search/movie?api_key=${key}&language=en-US&page=1&query=${params.id}&include_adult=false`
		);
		const data = await res.json();
		if (res.ok) {
			return {
				props: { searchedMovie: data.results }
			};
		}
	}
</script>

<script>
   import MovieCard from "../../components/MovieCard.svelte";
   export let searchedMovie;
</script>

<div class="searched-movies">
   {#each searchedMovie as movie}
      <MovieCard {movie}/>
   {/each}
</div>


<style>
   .searched-movies{
      display: grid;
      grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
      grid-column-gap: 1rem;
      grid-row-gap: 2rem;
      height: 20vh;
   }
</style>