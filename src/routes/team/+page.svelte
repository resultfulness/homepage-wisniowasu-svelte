<script lang="ts">
  import { onMount } from "svelte";

  import vanillatilt from "vanilla-tilt";
  import smoothscroll from "smoothscroll-polyfill";

  import { management, chairpeople } from "$lib/backend/team";
  import getIsMobile from "$lib/mobileExt";
  import TeamPicker from "./TeamPicker.svelte";
  import HumanCard from "./HumanCard.svelte";

  onMount(() => {
    smoothscroll.polyfill();

    const isMobile = getIsMobile();
    const isEdge = window.navigator.userAgent.indexOf("Edge") > -1;
    const items = document.querySelectorAll<HTMLDivElement>(".human-card");

    if (!isMobile && !isEdge) {
      vanillatilt.init([...items], {
        reverse: true, // reverse the tilt direction
        max: 10, // max tilt rotation (degrees)
        perspective: 1000, // Transform perspective, the lower the more extreme the tilt gets.
        speed: 1000, // Speed of the enter/exit transition
        transition: true, // Set a transition on enter/exit.
        reset: true, // If the tilt effect has to be reset on exit.
        scale: 1.1,
      });
    }

    ScrollReveal().reveal(items, {
      easing: "ease-in-out",
      distance: "20px",
    });
  });
</script>

<svelte:head>
  <title>Zespół - Wiśniowa SU | Samorząd Uczniowski</title>
</svelte:head>

<div class="title-box">
  <h1 class="title-box-text">
    ZESPÓŁ <span class="title-box-date">2022/23</span>
  </h1>
</div>
<div class="fullpadding" id="teamcontainer">
  <p class="category">Zarząd</p>

  <div class="human-cardcontainer">
    {#each management as person}
      <HumanCard {person} />
    {/each}
  </div>

  <div class="spacer" />
  <p class="category">Przewodniczący Sekcji</p>

  <div class="human-cardcontainer">
    {#each chairpeople as person}
      <HumanCard {person} />
    {/each}
  </div>
  <TeamPicker />
</div>

<style lang="scss">
  .human-cardcontainer {
    display: flex;
    flex-direction: row;
    flex-wrap: wrap;
    justify-content: center;
    align-content: flex-start;
    align-items: flex-start;
  }

  #teamcontainer {
    // display: grid;
    // grid-template-columns: repeat(2, 1fr);
    // grid-template-rows: 1fr;
    // grid-column-gap: 0px;
    // grid-row-gap: 0px;
    max-width: 1500px;
    margin: auto;

    .spacer {
      margin: 20px 20px 20px 20px;
      width: calc(100% - 40px);
      height: 1px;
      background-color: rgba(0, 0, 0, 0.3);
    }

    // p.gridleft
    // {
    //     grid-area: 1 / 1 / 2 / 2;
    // }
    // div.gridleft
    // {
    //     grid-area: 2 / 1 / 3 / 2;
    // }
    // p.gridright
    // {
    //     grid-area: 1 / 2 / 2 / 3;
    // }
    // div.gridright
    // {
    //     grid-area: 2 / 2 / 3 / 3;
    // }
  }

  p.category {
    font-weight: 700;
    margin: 0;
    font-size: 45px;
    color: black;
    text-transform: uppercase;
    justify-content: center;
    align-items: center;
    align-content: center;
    text-decoration: none;
    -webkit-animation: tracking-in-contract 0.8s
      cubic-bezier(0.215, 0.61, 0.355, 1) both;
    animation: tracking-in-contract 0.8s cubic-bezier(0.215, 0.61, 0.355, 1)
      both;

    text-align: center;
    padding: 20px 0 20px 0;
    background: linear-gradient(288deg, #ff7f66, #de1444);
    background-clip: text;
    -webkit-background-clip: text;
    -webkit-text-fill-color: transparent;

    @media (max-width: 450px) {
      font-size: 2.1em;
      height: auto;
    }
  }

  @keyframes tracking-in-contract {
    0% {
      letter-spacing: 1em;
      opacity: 0;
    }

    40% {
      opacity: 0.6;
    }

    100% {
      letter-spacing: normal;
      opacity: 1;
    }
  }
</style>
