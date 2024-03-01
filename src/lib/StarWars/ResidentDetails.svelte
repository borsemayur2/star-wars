<script>
  import { onMount } from "svelte";
  import { AccordionItem, Accordion, Spinner } from "flowbite-svelte";

  export let residentUrl;
  let resident = null;

  const fetchPlanets = async () => {
    const res = await fetch(residentUrl);
    const residentData = await res.json();
    resident = residentData;
  };
  onMount(fetchPlanets);
</script>

<AccordionItem>
  <span slot="header">
    {#if resident?.name}
      {resident?.name}
    {:else}
      Fetching... <Spinner />
    {/if}
  </span>
  <div class="container">
    <p>Height:{resident?.height}</p>
    <p>Mass:{resident?.mass}</p>
    <p>Gender:{resident?.gender}</p>
  </div>
</AccordionItem>
