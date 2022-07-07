<script context="module">
	export async function load({ fetch, params }) {
		const response = await fetch(
			`https://api.themoviedb.org/3/search/movie?api_key=${import.meta.env.VITE_API}&language=fr-FR&query=${params.id}`
		);
		const data = await response.json();
		if (response.ok) {
			return {
				props: { searchedMovie: data.results }
			};
		}
	}
</script>

<script>
	import MovieCard from '../../components/MovieCard.svelte';
    import {fly} from 'svelte/transition';
	export let searchedMovie;
</script>

<div class="searched-movies" in:fly={{ y: 50, duration: 500, delay: 500}} out:fly={{ duration: 500}}>
	{#each searchedMovie as movie}
		<MovieCard {movie} />
	{/each}
</div>

<style>
	.searched-movies {
		display: grid;
		grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
		column-gap: 1rem;
		row-gap: 2rem;
	}
</style>