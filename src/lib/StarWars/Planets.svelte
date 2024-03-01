<script>
  import { onMount } from "svelte";
  import { STAR_WARS_PLANETS_URL } from "../constants/constants";
  import PlanetDetails from "./PlanetDetails.svelte";
  import { Pagination } from "flowbite-svelte";
  import { Spinner } from "flowbite-svelte";

  let pages = [];

  let planets = [];
  let nextPageUrl = "";
  let previousPageUrl = "";

  const fetchPlanets = async (url) => {
    const res = await fetch(url);
    const planetsData = await res.json();
    planets = planetsData.results;
    nextPageUrl = planetsData.next;
    previousPageUrl = planetsData.previous;
    const totalPages = planetsData.count / 10;
    const newPages = [];
    for (let i = 1; i <= totalPages; i++) {
      const pageObject = {
        name: i,
      };
      newPages.push(pageObject);
    }
    pages = newPages;
  };
  onMount(() => fetchPlanets(STAR_WARS_PLANETS_URL));

  const handleClickNext = () => {
    if (nextPageUrl) fetchPlanets(nextPageUrl);
  };
  const handleClickPrevious = () => {
    if (previousPageUrl) fetchPlanets(previousPageUrl);
  };

  const handlePageClick = (e) => {
    const index = parseInt(e.target.innerText);
    const url = `${STAR_WARS_PLANETS_URL}?page=${index}&format=json`;
    fetchPlanets(url);
  };
</script>

{#if planets.length}
  <Pagination
    {pages}
    on:previous={handleClickPrevious}
    on:next={handleClickNext}
    on:click={handlePageClick}
  />
  <div class="container">
    {#each planets as planet}
      <PlanetDetails {planet} />
    {/each}
  </div>
{:else}
  <Spinner />
  <p>Loading planets...</p>
{/if}

<style>
  .container {
    margin: auto;
    display: flex;
    flex-flow: wrap;
    gap: 10px;
  }
</style>
