<script lang="ts">
  import type { PersonCardData } from "$lib/types";

  export let person: PersonCardData;

  const { title, name, info, imgSrc, icon } = person;

  let isOpened = false;
</script>

<!-- svelte-ignore a11y-click-events-have-key-events -->
<div
  class="human-card"
  class:open={isOpened}
  class:disp={isOpened}
  on:click={() => (isOpened = isOpened === false ? true : false)}
  on:mouseleave={() => (isOpened = false)}
>
  <img src={imgSrc} alt={name} class="personimg" />
  <div class="info">
    <img src={icon} alt="" />
    <div class="box">
      <p class="title">{title}</p>
      <p class="name">{name}</p>
    </div>
  </div>
  <div class="moreinfo">
    {info}
  </div>
</div>

<style lang="scss">
  .human-card {
    width: 350px;
    height: 400px;
    box-shadow: 0 0 20px rgba(0, 0, 0, 0.3);
    margin: 20px;
    display: grid;
    grid-template-columns: auto;
    grid-template-rows: 300px 100px;
    grid-column-gap: 0;
    grid-row-gap: 0;
    transform-style: preserve-3d;
    border-radius: 5px;
    cursor: pointer;

    &.open:not(.hover) {
      .moreinfo {
        opacity: 1;
        background-color: white;
        margin-top: 19px;
        transform: translate3d(0, -6px, 30px);
      }

      .info {
        border-radius: 0;
        margin: 11px 11px 7px 11px !important;
        padding-bottom: 4px;
        transform: translate3d(0, -6px, 30px);

        @supports (-ms-ime-align: auto) {
          margin: 11px 11px 11px 11px !important;
          padding-bottom: 0;
          transform: translate3d(0, 0, 30px);
        }
      }
    }

    &.open.hover {
      .moreinfo {
        opacity: 1;
        background-color: white;
        margin: 10px 8px -15px 8px;
        transform: translateZ(30px);
      }
    }

    &.open {
      transform: scale(1.1) !important;
    }

    .moreinfo {
      grid-area: 1 / 1 / 2 / 2;
      z-index: 3;
      opacity: 0;
      margin: 312px 11px -12px 11px;
      padding: 15px;
      transition: all 0.2s ease-in-out;
      overflow-y: scroll;
      -webkit-overflow-scrolling: touch;

      @supports (-ms-ime-align: auto) {
        margin: 319px 11px -19px 11px;
      }
    }

    .info {
      margin: 15px;
      grid-area: 2 / 1 / 3 / 2;
      z-index: 2;
      background-color: white;
      border-radius: 5px;
      box-shadow: 0 0 20px rgba(0, 0, 0, 0.3);

      transition: all 0.2s ease-in-out;

      display: grid;
      grid-template-columns: 70px 1fr;
      grid-template-rows: auto;
      grid-column-gap: 0;
      grid-row-gap: 0;

      overflow: hidden;

      img {
        grid-area: 1 / 1 / 2 / 2;
        width: calc(100% - 30px);
        height: calc(100% - 30px);
        padding: 15px;
        object-position: center;
        object-fit: contain;
        filter: drop-shadow(0 0 10px rgba(0, 0, 0, 0.15));
        pointer-events: none;
        overflow: hidden;
      }

      div.box {
        display: flex;
        flex-direction: column;
        flex-wrap: nowrap;
        justify-content: center;
        align-content: flex-start;
        align-items: flex-start;
        // fixes a weird bug when sometimes the height doesn't automatically set
        // to 70px and stays 100px until hover event happens
        height: 70px;
        padding-left: 10px;
      }

      p {
        &.title {
          font-family: "Raleway", sans-serif;
          margin: 0;
          font-size: 13px;
          font-weight: 600;

          color: rgba(0, 0, 0, 0.7);

          @media (max-width: 425px) {
            font-size: 10px;
          }
        }

        &.name {
          margin: 0;
          font-size: 20px;
          font-weight: 600;

          @media (max-width: 425px) {
            font-size: 18px;
          }
        }
      }
    }

    img.personimg {
      object-fit: cover;
      width: 100%;
      height: 100%;
      object-position: center;
      grid-area: 1 / 1 / 3 / 2;
      z-index: 1;
      pointer-events: none;
    }

    &.hover {
      .info {
        border-radius: 0;
        margin: 8px;
        transform: translate3d(0, 0, 30px);
      }

      transform: scale(1.08) !important;
    }
  }

  @media (hover: hover) {
    .human-card:hover {
      .info {
        border-radius: 0;
        margin: 11px;
        transform: translate3d(0, -6px, 30px);

        @supports (-ms-ime-align: auto) {
          transform: translate3d(0, 0, 30px);
        }
      }

      @supports (-ms-ime-align: auto) {
        transform: scale(1.05) !important;
      }
    }
  }
</style>
