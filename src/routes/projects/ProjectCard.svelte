<script lang="ts">
  import { createEventDispatcher } from "svelte";

  export let project: {
    date: string;
    imgSrc: string;
    title: string;
    text: string;
    imgStyle?: string;
  };

  const { date, imgSrc, imgStyle, title, text } = project;

  const dispatch = createEventDispatcher();

  function handleClick(
    event: MouseEvent & { currentTarget: EventTarget & HTMLDivElement }
  ): void {
    dispatch("clicked", { event: event });
  }
</script>

<div class="timeline-card">
  <div class="date">{date}</div>
  <div class="container">
    <!-- svelte-ignore a11y-click-events-have-key-events -->
    <div class="img-container" on:click={handleClick}>
      <img src={imgSrc} alt={title} style={imgStyle} />
    </div>
    <div class="title">{title}</div>
    <div class="text">{text}</div>
  </div>
</div>

<style lang="scss">
  .timeline-card {
    min-height: 100px;
    margin-bottom: 40px;

    margin-left: 20px;
    margin-right: 20px;

    div.date {
      //changes allow multiline dates on mobile
      //height: 80px;
      //margin-left: 64px;
      height: auto;
      margin: 25px 0 25px 64px;
      font-size: 26px;
      //line-height: 80px;
      vertical-align: middle;
      font-weight: 700;
      color: rgba(0, 0, 0, 0.3);
    }

    div.container {
      position: relative;

      // display: grid;
      // grid-template-columns: 45% 1fr;
      // grid-template-rows: 70px auto auto;
      // grid-column-gap: 0px;
      // grid-row-gap: 0px;
      div.img-container {
        position: relative;
        border-radius: 20px;
        overflow: hidden;
        height: 250px;
        box-shadow: 0 0 10px rgba(0, 0, 0, 0.4);
        transition: transform 0.3s ease-in-out !important;
        transform: scale(1.075) !important;
        z-index: 1;
        cursor: pointer;

        img {
          width: 100%;
          height: 100%;
          object-fit: cover;
          background-position: center;
        }
      }

      @media (hover: hover) {
        div.img-container:hover {
          transform: scale(1.05) !important;
        }
      }

      div.img-container::after {
        content: "";
        position: absolute;
        left: 0;
        bottom: 0;
        width: 100%;
        height: 100%;
        background: linear-gradient(
          7deg,
          rgba(0, 0, 0, 1) 0%,
          rgba(100, 100, 100, 0) 60%,
          rgba(255, 255, 255, 0) 100%
        );
      }

      div.title {
        position: absolute;
        display: flex;
        height: 230px;
        width: calc(100% - 40px);
        top: 0;
        left: 0;
        align-items: flex-end;
        padding: 0 20px 20px 20px;
        color: rgba(255, 255, 255, 1);
        font-size: 30px;
        font-weight: 700;
        font-family: "Raleway", sans-serif;
        pointer-events: none;
        z-index: 1;
      }

      div.text {
        overflow: hidden;
        padding: 20px;
        max-height: 1000px;
        color: rgba(0, 0, 0, 0.8);
        font-size: 14px;
        transition: opacity 0.2s ease-in-out, max-height 0.2s ease-in-out,
          padding 0.2s ease-in-out;
        z-index: 0;
        box-shadow: 0 0 20px rgba(0, 0, 0, 0.2);
        border-bottom-left-radius: 10px;
        border-bottom-right-radius: 10px;
        background: white;
      }
    }

    div.container:not(.open) {
      div.text {
        opacity: 0;
        max-height: 0;
        padding: 0 20px;
      }

      div.img-container {
        transform: scale(1) !important;
      }

      @media (hover: hover) {
        div.img-container:hover {
          transform: scale(1.05) !important;
        }
      }
    }
  }
</style>
