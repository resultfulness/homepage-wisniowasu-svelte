<script lang="ts">
  import { routes } from "$lib/backend/routes";

  export let isNavBtnBackgroundShown: boolean;
  export let isLogoNotShown: boolean;
  export let currentPage: string;
  let isNavActive = false;
</script>

<header class="cd-header">
  <div
    class="nav-logo"
    class:nav-bg={isNavBtnBackgroundShown}
    class:nologo={isLogoNotShown}
  >
    <div class="nav-logo-image" />
  </div>
  <div
    class="nav-but-wrap"
    class:nologo={isLogoNotShown}
    class:nav-bg={isNavBtnBackgroundShown}
  >
    <!-- svelte-ignore a11y-click-events-have-key-events -->
    <div
      class="menu-icon hover-target"
      on:click={() => (isNavActive = !isNavActive)}
    >
      <span
        class="menu-icon__line menu-icon__line-left"
        class:nav-bg={isNavBtnBackgroundShown}
        class:nav-active={isNavActive}
      />
      <span
        class="menu-icon__line"
        class:nav-bg={isNavBtnBackgroundShown}
        class:nav-active={isNavActive}
      />
      <span
        class="menu-icon__line menu-icon__line_last menu-icon__line-right"
        class:nav-bg={isNavBtnBackgroundShown}
        class:nav-active={isNavActive}
      />
    </div>
  </div>
  <div class="nav" class:nav-active={isNavActive}>
    <div class="nav__content" class:nav-active={isNavActive}>
      <ul class="nav__list">
        {#each [...routes] as [route, title]}
          <!-- svelte-ignore a11y-click-events-have-key-events -->
          <li
            class="nav__list-item"
            class:nav-active={isNavActive}
            class:active-nav={currentPage === route}
          >
            <a href={route}>{title}</a>
          </li>
        {/each}
      </ul>
    </div>
  </div>
</header>

<style lang="scss">
  $logo_url: url(/img/logos/logo_title.png);
  $imagew: 312px;
  $imagewandmenu: $imagew + 80px;
  $radius: 30px;

  .cd-header {
    position: fixed;
    height: 100%;
    width: 100%;
    top: 0;
    left: 50%;
    transform: translateX(-50%);
    max-width: 1500px;
    z-index: 9999;
    display: grid;
    grid-template-columns: 1fr 80px;
    grid-template-rows: 80px;
    grid-column-gap: 0;
    grid-row-gap: 0;
    pointer-events: none;
  }

  .nav-but-wrap {
    grid-area: 1 / 2 / 2 / 3;
    position: relative;
    pointer-events: all;
    display: inline-flex;
    float: right;
    justify-content: center;
    height: 80px;
    width: 80px;
    transition: border-radius linear 0.8s, background-color 0.3s ease;
    border-bottom-left-radius: $radius;

    @media (min-width: 1500px) {
      border-bottom-right-radius: $radius;
    }
  }

  .nav-but-wrap::before {
    opacity: 0;
    content: "";
    width: 80px;
    height: 80px;
    border-bottom-left-radius: $radius;
    z-index: -10;
    position: absolute;
    box-shadow: 0 0 20px 0 rgba(0, 0, 0, 0.5);
    transition: border-radius linear 0.8s, box-shadow 0.3s ease;

    @media (min-width: 1500px) {
      border-bottom-right-radius: $radius;
    }
  }

  .nav-logo-image {
    background-image: $logo_url;
    background-size: contain;
    background-position: center;
    background-repeat: no-repeat;
    width: calc(100% - 10px);
    height: calc(100% - 10px);
    margin: 3px 5px 7px 5px;
  }

  .nav-logo {
    opacity: 0;
    grid-area: 1 / 1 / 2 / 2;
    box-sizing: border-box;
    background-color: white;
    max-width: #{$imagew};
    height: 80px;
    transform: translateY(-100px);
    border-bottom-right-radius: $radius;
    transition: border-radius linear 0.8s, opacity 0.3s ease,
      transform 0.3s ease, color 0.3s ease, -webkit-transform 0.3s ease;

    @media (min-width: 1500px) {
      border-bottom-left-radius: $radius;
    }

    @media (max-width: $imagewandmenu) {
      border-bottom-right-radius: 0;
    }
  }

  .nav-logo::before {
    position: absolute;
    grid-area: 1 / 1 / 2 / 2;
    content: "";
    z-index: -10;
    box-sizing: border-box;
    width: 100%;
    max-width: #{$imagew};
    height: 80px;
    border-bottom-right-radius: $radius;
    box-shadow: 0 0 20px 0 rgba(0, 0, 0, 0.5);
    transition: border-radius linear 0.8s;

    @media (min-width: 1500px) {
      border-bottom-left-radius: $radius;
    }

    @media (max-width: $imagewandmenu) {
      border-bottom-right-radius: 0;
    }
  }

  .nav-but-wrap:not(.nologo) {
    @media (max-width: $imagewandmenu) {
      border-bottom-left-radius: 0;
    }
  }

  .nav-but-wrap:not(.nologo)::before {
    @media (max-width: $imagewandmenu) {
      border-bottom-left-radius: 0;
    }
  }

  .nav-but-wrap.nav-bg {
    background-color: white;
  }

  .nav-but-wrap.nav-bg::before {
    opacity: 1;
  }

  .menu-icon__line.nav-bg {
    background-color: black;
  }

  .nav-logo.nav-bg:not(.nologo) {
    opacity: 1;
    transform: translateY(0);
  }

  .menu-icon {
    width: 30px;
    position: relative;
    z-index: 2;
    cursor: pointer;
    align-self: center;
    display: block;
  }

  .menu-icon__line {
    height: 2px;
    width: 30px;
    display: block;
    background-color: white;
    margin-bottom: 7px;
    cursor: pointer;
    transition: background-color 0.5s ease;
    transition: transform 0.2s ease, background-color 0.5s ease;
    transition: transform 0.2s ease, background-color 0.5s ease;
  }

  .menu-icon__line_last {
    margin-bottom: 0;
  }

  .menu-icon__line-left {
    width: 16.5px;
    transition: all 200ms linear;
  }

  .menu-icon__line-right {
    width: 16.5px;
    float: right;
    transition: all 200ms linear;
  }

  .menu-icon:hover .menu-icon__line-left,
  .menu-icon:hover .menu-icon__line-right {
    width: 30px;
  }

  .nav {
    position: fixed;
    z-index: 1;
    pointer-events: all;
  }

  .nav::before,
  .nav::after {
    content: "";
    position: fixed;
    top: 10px;
    right: 10px;
    width: 0;
    height: 0;
    background-color: rgba(20, 21, 26, 0.6);
    border-bottom-left-radius: 200%;
    z-index: -1;
    transition: border-radius ease 0.8s,
      width cubic-bezier(0.77, 0, 0.175, 1) 0.6s,
      height cubic-bezier(0.77, 0, 0.175, 1) 0.6s;
  }

  .nav::after {
    background-color: white;
    background-position: bottom center;
    background-repeat: no-repeat;
    background-size: 300%;
    transition-delay: 0s;
    box-shadow: 6px 7px 28px 0 rgba(16, 16, 16, 0.3);
  }

  .nav::before {
    transition-delay: 0.2s;
  }

  .nav__content {
    position: fixed;
    visibility: hidden;
    top: 90px;
    right: 10px;
    width: 300px;
    text-align: left;
  }

  .nav__list {
    position: relative;
    padding: 0;
    margin: 0;
    z-index: 2;
  }

  .nav__list-item {
    position: relative;
    display: block;
    opacity: 0;
    text-align: left;
    color: #fff;
    overflow: hidden;
    font-family: "Poppins", sans-serif;
    font-size: 22px;
    line-height: 1.2;
    letter-spacing: 2px;
    transform: translate(30px, 0%);
    transition: opacity 0.1s ease, transform 0.2s ease;
    transition-delay: 0.2s;
    margin-top: 7px;
    margin-bottom: 7px;
  }

  .nav__list-item a {
    position: relative;
    text-decoration: none;
    color: black;
    overflow: hidden;
    cursor: pointer;
    font-family: "Poppins", sans-serif;
    font-weight: 600;
    z-index: 2;
    height: 28px;
    padding-left: 40px;
    padding-top: 5px;
    padding-bottom: 5px;
    display: inline-block;
    transition: all 200ms linear;
  }

  .nav__list-item a::after {
    position: absolute;
    content: "";
    top: 50%;
    left: 0;
    width: 5px;
    height: 0;
    opacity: 0;
    background: linear-gradient(288deg, #ff7f66, #de1444);
    z-index: 1;
    transition: all 200ms linear;
  }

  .nav__list-item a:hover::after {
    height: 100%;
    opacity: 1;
    top: 0;
  }

  .nav__list-item:not(.active-nav) a:hover {
    color: #770303;
    font-size: 23px;
    transition: color 100ms ease-in-out, font-size 100ms ease-in-out;
  }

  .nav__list-item.active-nav a {
    background: linear-gradient(288deg, #ff7f66, #de1444);
    background-clip: text;
    font-size: 25px;
    -webkit-background-clip: text;
    -webkit-text-fill-color: transparent;
  }

  .nav__list-item.active-nav a::after {
    height: 100%;
    opacity: 1;
    top: 0;
  }

  .nav__content.nav-active {
    visibility: visible;
  }

  .menu-icon__line.nav-active {
    background-color: black;
    transform: translate(0, 0) rotate(-45deg);
  }

  .menu-icon__line-left.nav-active {
    width: 15px;
    -webkit-transform: translate(2px, 4px) rotate(45deg);
    transform: translate(2px, 4px) rotate(45deg);
  }

  .menu-icon__line-right.nav-active {
    width: 15px;
    float: right;
    transform: translate(-3px, -3.5px) rotate(45deg);
  }

  .menu-icon:hover
    :is(.menu-icon__line-left, .menu-icon__line-right).nav-active {
    width: 15px;
  }

  .nav.nav-active {
    visibility: visible;
  }

  .nav.nav-active::after,
  .nav.nav-active::before {
    width: 300px;
    height: 400px;
    border-radius: 15px;
  }

  .nav.nav-active::after {
    transition-delay: 0.1s;
  }

  .nav.nav-active::before {
    transition-delay: 0s;
  }

  .nav__list-item.nav-active {
    opacity: 1;
    transform: translateX(0%);
    transition: opacity 0.3s ease, color 0.3s ease;
    transition: opacity 0.3s ease, transform 0.3s ease, color 0.3s ease;
    transition: opacity 0.3s ease, transform 0.3s ease, color 0.3s ease;
  }

  .nav__list-item.nav-active:nth-child(0) {
    -webkit-transition-delay: 0.4s;
    transition-delay: 0.4s;
  }

  .nav__list-item.nav-active:nth-child(1) {
    -webkit-transition-delay: 0.5s;
    transition-delay: 0.5s;
  }

  .nav__list-item.nav-active:nth-child(2) {
    -webkit-transition-delay: 0.6s;
    transition-delay: 0.6s;
  }

  .nav__list-item.nav-active:nth-child(3) {
    -webkit-transition-delay: 0.7s;
    transition-delay: 0.7s;
  }

  .nav__list-item.nav-active:nth-child(4) {
    -webkit-transition-delay: 0.8s;
    transition-delay: 0.8s;
  }

  .nav__list-item.nav-active:nth-child(5) {
    -webkit-transition-delay: 0.9s;
    transition-delay: 0.9s;
  }

  .nav__list-item.nav-active:nth-child(6) {
    -webkit-transition-delay: 1s;
    transition-delay: 1s;
  }

  .nav__list-item.nav-active:nth-child(7) {
    -webkit-transition-delay: 1.1s;
    transition-delay: 1.1s;
  }

  .nav__list-item.nav-active:nth-child(8) {
    -webkit-transition-delay: 1.2s;
    transition-delay: 1.2s;
  }

  .nav__list-item.nav-active:nth-child(9) {
    -webkit-transition-delay: 1.3s;
    transition-delay: 1.3s;
  }

  .nav__list-item.nav-active:nth-child(10) {
    -webkit-transition-delay: 1.4s;
    transition-delay: 1.4s;
  }
</style>
