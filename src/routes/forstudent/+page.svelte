<script lang="ts">
  import { onMount } from "svelte";

  import { services } from "$lib/content/forstudent.json";
  import ServiceCard from "./ServiceCard.svelte";

  onMount(() => {
    var items = document.querySelectorAll(".service-card");
    ScrollReveal().reveal(items, {
      easing: "ease-in-out",
      distance: "20px",
    });
  });
</script>

<svelte:head>
  <title>Dla ucznia - Wiśniowa SU | Samorząd Uczniowski</title>
</svelte:head>

<div class="title-box">
  <h1 class="title-box-text">DLA UCZNIA</h1>
</div>
<div id="services-container">
  {#each services as service}
    <ServiceCard {service} />
  {/each}
</div>

<style lang="scss">
  #services-container {
    display: flex;
    flex-direction: row;
    flex-wrap: wrap;
    justify-content: center;
    align-content: flex-start;
    align-items: flex-start;
    max-width: 1500px;
    margin: auto;
  }
</style>
