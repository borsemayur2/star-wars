<script>
  import { Card } from "flowbite-svelte";
  import Residents from "./Residents.svelte";
  export let planet;
</script>

{#if planet}
  <Card>
    <div>
      <div class="planetData">
        <h5
          class="mb-2 text-2xl font-bold tracking-tight text-gray-900 dark:text-white"
        >
          {planet.name}
        </h5>
        <h5>Climate: {planet.climate}</h5>
        <h5>Population: {planet.population}</h5>
        <h5>Terrains: {planet.terrain}</h5>
      </div>
      <hr
        class="my-2 border-gray-200 sm:mx-auto dark:border-gray-700 lg:my-4"
      />
      <h4
        class="mb-2 text-2xl font-bold tracking-tight text-gray-900 dark:text-white"
      >
        Residents
      </h4>
      <Residents residents={planet.residents} />
    </div>
  </Card>
{/if}

<style>
  .planetData {
    height: 120px;
  }
</style>
