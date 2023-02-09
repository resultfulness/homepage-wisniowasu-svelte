<script lang="ts">
  import { onMount } from "svelte";

  import smoothscroll from "smoothscroll-polyfill";

  import { projects } from "$lib/backend/projects";
  import ProjectCard from "./ProjectCard.svelte";

  onMount(() => {
    smoothscroll.polyfill();

    ScrollReveal().reveal(document.querySelectorAll(".container"), {
      easing: "ease-in-out",
      distance: "20px",
    });
  });

  function handleOpen(
    event: MouseEvent & { currentTarget: EventTarget & HTMLDivElement }
  ): void {
    let wasAnItemOpen = false;

    [...document.querySelectorAll(".img-container")]
      .filter((el) => el !== event.currentTarget)
      .forEach((el) => {
        if (el.parentElement?.classList.contains("open")) wasAnItemOpen = true;
        el.parentElement?.classList.remove("open");
      });

    const parent = event.currentTarget.parentElement;

    parent?.classList.toggle("open");

    if (parent?.classList.contains("open")) {
      if (wasAnItemOpen) {
        setTimeout(() => {
          parent?.scrollIntoView({
            block: "center",
            behavior: "smooth",
          });
        }, 201);
      } else {
        parent?.scrollIntoView({
          block: "center",
          behavior: "smooth",
        });
      }
    }
  }
</script>

<svelte:head>
  <title>Projekty - Wiśniowa SU | Samorząd Uczniowski</title>
</svelte:head>

<div class="title-box">
  <h1 class="title-box-text">PROJEKTY</h1>
</div>
<div class="pageblock-timeline">
  <div id="timeline-line" />
  <div id="timeline-container">
    {#each projects as project}
      <ProjectCard
        {project}
        on:clicked={(dispatchedEvent) =>
          handleOpen(dispatchedEvent.detail.event)}
      />
    {/each}
  </div>
</div>

<style lang="scss">
  #timeline {
    &-line {
      position: fixed;
      z-index: -1;
      background-color: rgba(0, 0, 0, 0.3);
      width: 4px;
      height: 100%;
      margin-left: 60px;
      margin-top: -260px;
      padding-bottom: 260px;

      @media (max-width: 435px) {
        margin-left: 40px;
      }
    }
  }

  .pageblock-timeline {
    position: relative;
    max-width: 700px;

    margin: 0 auto;
  }
</style>
