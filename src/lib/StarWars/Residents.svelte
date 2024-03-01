<script>
  import { AccordionItem, Accordion } from "flowbite-svelte";
  import ResidentDetails from "./ResidentDetails.svelte";

  export let residents;
</script>

{#if residents}
  <Accordion>
    {#each residents as residentUrl}
      <ResidentDetails {residentUrl} />
    {/each}
  </Accordion>
{/if}
