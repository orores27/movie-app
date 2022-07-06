<script context="module">
    export async function load({fetch}) {
        const response = await fetch(`https://api.themoviedb.org/3/movie/popular?api_key=d87d9bd9cbb63454314c8992f55cab0c&language=fr-FR`);
        const data = await response.json();
        if(response.ok) {
            return {
                props: {popular: data.results}
            };
        };
    };
</script>

<script>
    import PopularMovies from "../components/PopularMovies.svelte";
    import SearchMovies from "../components/SearchMovies.svelte";
    export let popular;
</script>

<section>
    <SearchMovies />
    <PopularMovies {popular} />
</section>