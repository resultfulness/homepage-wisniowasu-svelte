<script lang="ts">
  import { onMount } from "svelte";

  import vanillatilt from "vanilla-tilt";
  import scrollreveal from "scrollreveal";

  import { aboutUs, noteworthy, strengths, sections } from "$lib/backend/home";
  import getIsMobile from "$lib/mobileExt";

  onMount(() => {
    var isMobile = getIsMobile();
    // let isMobile = false;

    if (!isMobile) {
      vanillatilt.init(document.querySelector("#logo") as HTMLDivElement, {
        reverse: true, // reverse the tilt direction
        max: 10, // max tilt rotation (degrees)
        perspective: 1000, // Transform perspective, the lower the more extreme the tilt gets.
        speed: 1000, // Speed of the enter/exit transition
        transition: true, // Set a transition on enter/exit.
        reset: true, // If the tilt effect has to be reset on exit.
        "full-page-listening": true,
      });
    }

    var items = document.querySelectorAll(".card");
    var items2 = document.querySelectorAll(".minicard");
    var items3 = document.querySelectorAll(".button");
    scrollreveal().reveal(items, {
      easing: "ease-in-out",
      distance: "20px",
    });
    scrollreveal().reveal(items2, {
      easing: "ease-in-out",
      distance: "20px",
    });
    scrollreveal().reveal(items3, {
      easing: "ease-in-out",
      distance: "20px",
    });
  });
</script>

<svelte:head>
  <title>Wiśniowa SU | Samorząd Uczniowski</title>
</svelte:head>

<div id="logo-container">
  <div id="logo" />
  <svg
    id="slide-down-icon"
    viewBox="0 0 247 390"
    version="1.1"
    xmlns="http://www.w3.org/2000/svg"
    xmlns:xlink="http://www.w3.org/1999/xlink"
  >
    <path
      id="wheel"
      d="M123.359,79.775l0,72.843"
      style="fill:none;stroke:#fff;stroke-width:20px;"
    />
    <path
      id="mouse"
      d="M236.717,123.359c0,-62.565 -50.794,-113.359 -113.358,-113.359c-62.565,0 -113.359,50.794 -113.359,113.359l0,143.237c0,62.565 50.794,113.359 113.359,113.359c62.564,0 113.358,-50.794 113.358,-113.359l0,-143.237Z"
      style="fill:none;stroke:#fff;stroke-width:20px;"
    />
  </svg>
  <div id="slide-down-text">Zjedź na dół by dowiedzieć się więcej</div>
  <div id="team-image-container">
    <div id="moving-gradient" />
    <a
      id="team-image"
      data-href="/img/team/2021_22/team.jpg?size=1920"
      class="progressive replace"
    >
      <img
        src="/img/team/2021_22/team.jpg?size=100"
        alt="Zespół"
        class="preview"
      />
    </a>
  </div>
</div>
<h1 class="section-topic">O nas</h1>
<div class="pageblock-full">
  <div class="card">
    <div class="card-image" />
    <h2 class="card-title">O nas</h2>
    <h3 class="card-text">
      {aboutUs}
    </h3>
  </div>
</div>
<h2 class="section-topic">Warte uwagi</h2>
<div class="pageblock-full">
  <div class="buttonsgroup">
    {#each noteworthy as { href, imgSrc, imgAlt, text }}
      <a {href} class="button">
        <div class="img-container">
          <img data-src={imgSrc} alt={imgAlt} class="lazyload" />
        </div>
        <h3 class="button-text">{text}</h3>
      </a>
    {/each}
  </div>
</div>
<h2 class="section-topic">Nasze atuty</h2>
<div class="pageblock-full">
  <div class="cardgroup">
    {#each strengths as { name, description, icon, iconAlt }}
      <div class="minicard">
        <img class="minicard-icon lazyload" alt="{iconAlt}," data-src={icon} />
        <h3 class="minicard-title">{name}</h3>
        <h3 class="minicard-text">{description}</h3>
      </div>
    {/each}
  </div>
</div>
<h2 class="section-topic">Nasze sekcje</h2>
<div class="pageblock-full">
  <div class="cardgroup">
    {#each sections as { name, description, icon, iconAlt }}
      <div class="minicard short">
        <img class="minicard-icon lazyload" alt={iconAlt} data-src={icon} />
        <h3 class="minicard-title">{name}</h3>
        <h3 class="minicard-text">{description}</h3>
      </div>
    {/each}
  </div>
</div>

<style lang="scss">
  @import "$lib/scss/shadows.scss";

  $imageurl: url("/img/team/2019_20/team.jpg?size=1920");

  @function strip-unit($number) {
    @if type-of($number) == "number" and not unitless($number) {
      @return $number / ($number * 0 + 1);
    }

    @return $number;
  }

  #logo {
    background-image: url(/img/logos/logo_2019.png);
    width: 75%;
    resize: both;
    height: 50%;
    max-width: 624px;
    max-height: 624px;
    background-size: contain;
    background-repeat: no-repeat;
    background-position: center;
    z-index: 1;
  }

  #logo-container {
    width: 100%;
    height: 100vh;
    display: flex;
    align-items: center;
    justify-content: center;
    overflow: hidden;
  }

  #slide-down-text {
    opacity: 0.7;
    position: absolute;
    bottom: 40px;
    color: white;
    z-index: 1;
  }

  #slide-down-icon {
    height: 30px;
    opacity: 0.7;
    position: absolute;
    bottom: 80px;
    color: white;
    z-index: 1;
    fill-rule: evenodd;
    clip-rule: evenodd;
    stroke-linecap: round;
    stroke-linejoin: round;
    stroke-miterlimit: 1.5;

    @media (max-height: 400px) {
      height: 20px;
    }

    #wheel {
      animation: scroll ease 1.5s infinite;
    }
  }

  @keyframes scroll {
    0% {
      transform: translateY(0);
    }

    30% {
      transform: translateY(40px);
    }
  }

  #team-image-container {
    position: absolute;
    width: 100%;
    height: 100vh;
    overflow: hidden;
  }

  #team-image {
    width: 100vw;
    background-size: cover;
    background-position: center;
    // background-image: $imageurl;
    filter: brightness(70%) grayscale(40%);
    height: 100vh;
    background-repeat: no-repeat;
    z-index: 0;
    opacity: 0.3;

    img {
      height: 100%;
      object-fit: cover;
    }
  }

  #logo-container + .section-topic {
    margin-top: 20px;
  }

  .minicard {
    @include shadow("nonclikable");
    background-color: white;
    width: 260px;
    height: 420px;
    padding: 20px;
    margin: 20px;
    border-radius: 40px;
    display: flex;
    flex-direction: column;
    flex-wrap: nowrap;
    justify-content: center;
    align-content: stretch;
    align-items: center;

    &.short {
      height: 320px;
    }

    &-icon {
      margin-top: 5px;
      height: 100px;
    }

    &-title {
      font-family: "Raleway", sans-serif;
      margin: 20px 0 20px 0;
      font-size: 18px;
      font-weight: 600;
      text-transform: uppercase;
    }

    &-text {
      font-size: 14px;

      text-align: center;
      margin: 0 auto auto auto;
    }

    @media (max-width: 696px) {
      height: unset;
    }
  }

  .cardgroup {
    display: flex;
    flex-wrap: wrap;
    justify-content: center;
    align-items: center;
    align-content: center;
    width: 100%;
    max-width: 1020px;
    margin: -20px 0;

    @media (max-width: 696px) {
      overflow: hidden;
    }
  }

  // There is no image-width or image-height ????
  // $imagew: image-width($imageurl);
  // $imageh: image-height($imageurl);
  // $imagew_l: strip-unit($imagew);
  // $imageh_l: strip-unit($imageh);

  // thus, hardcoded
  $imagew_l: 4604;
  $imageh_l: 3464;

  // also can't seem to get this to work so
  // @media (max-aspect-ratio: #{$imagew_l} / #{$imageh_l}) {
  @media (max-aspect-ratio: 4604 / 3464) {
    #team-image {
      background-size: auto 100%;
      width: calc(100vh / #{$imageh_l} * #{$imagew_l});
      background-position: left;
      animation: movingbg 40s ease-in-out infinite;
      will-change: transform;
    }
  }

  @keyframes movingbg {
    0% {
      transform: translateX(0);
    }

    50% {
      transform: translateX(calc(100vw - 100vh / #{$imageh_l} * #{$imagew_l}));
    }

    100% {
      transform: translateX(0);
    }
  }

  #moving-gradient {
    position: absolute;
    width: 100vw;
    height: 100vh;
    background: radial-gradient(
      #ff7f66,
      #a70028
    ); //radial-gradient(#ff7f66, #ef4058);
    animation: moving 8s ease-in-out infinite;
    transform-style: preserve-3d;
    backface-visibility: hidden;
    overflow: hidden;
  }

  @keyframes moving {
    0% {
      transform: scale3d(1, 1, 1);
    }

    50% {
      transform: scale3d(2, 2, 1);
    }

    100% {
      transform: scale3d(1, 1, 1);
    }
  }

  .card {
    @include shadow("nonclikable");
    margin-left: 20px;
    margin-right: 20px;
    background-color: white;
    border-radius: 20px;
    width: 100%;
    max-width: 1080px;
    display: grid;
    grid-template-columns: 1fr 1fr;
    grid-template-rows: 70px auto auto;
    grid-column-gap: 0;
    grid-row-gap: 0;
    overflow: hidden;

    &-image {
      grid-area: 1 / 1 / 4 / 2;
      background-image: url("/img/team/2021_22/alt_team.jpg?size=920");
      background-size: cover;
      background-repeat: no-repeat;
      background-position: center;
      aspect-ratio: 920/613;
    }

    &-text {
      //grid-area: 2 / 2 / 4 / 3;
      grid-area: 1 / 2 / 4 / 3;
      padding: 20px;
    }

    &-title {
      display: none;

      grid-area: 1 / 2 / 2 / 3;
      //display: flex;
      flex-direction: column;
      justify-content: flex-end;
      padding-left: 20px;
      padding-top: 20px;
      font-size: 35px;
    }

    @media (max-width: 1100px) {
      grid-template-rows: auto auto auto;

      &-image {
        min-height: 200px;
        grid-area: 1 / 1 / 2 / 3;
      }

      &-text {
        grid-area: 3 / 1 / 4 / 3;
      }

      &-title {
        grid-area: 2 / 1 / 3 / 3;
      }
    }
  }

  .buttonsgroup {
    display: flex;
    flex-wrap: wrap;
    justify-content: center;
    align-items: center;
    align-content: center;
    width: 100%;
    max-width: 1020px;
    margin: -20px 0;

    a.button {
      width: 470px;
      margin: 20px;
      position: relative;

      @media (max-width: 1036px) {
        max-width: 640px;
        width: 100%;
      }

      div.img-container {
        @include shadow("button");
        position: relative;
        border-radius: 20px;
        overflow: hidden;
        background-color: white;
        height: 150px;
        transition: transform 0.225s ease-in-out !important;
        transform: scale(1) !important;
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

      .button-text {
        position: absolute;
        display: flex;
        height: 130px;
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
    }
  }
</style>
