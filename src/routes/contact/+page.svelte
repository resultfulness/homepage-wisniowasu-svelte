<script lang="ts">
  import { onMount } from "svelte";

  import scrollreveal from "scrollreveal";

  onMount(() => {
    var items = document.querySelectorAll(".slideable");
    scrollreveal().reveal(items, {
      easing: "ease-in-out",
      distance: "20px",
    });
  });
</script>

<svelte:head>
  <title>Kontakt - Wiśniowa SU | Samorząd Uczniowski</title>
</svelte:head>

<div class="title-box">
  <h1 class="title-box-text">KONTAKT</h1>
</div>
<div class="fullpadding" id="contact-container">
  <div class="smallbox slideable">
    <div class="data">
      <p class="title">Napisz maila</p>
      <br />
      <p class="subtitle">Kontakowy adres mailowy SU</p>
      <a href="mailto:su@tm1.edu.pl">kontakt@wisniowasu.pl</a>
      <br /><br />
      <p class="subtitle">Administrator IT</p>
      Maciej Tracz
      <br />
      <a href="mailto:maciej.tracz@tm1.edu.pl">maciej.tracz@tm1.edu.pl</a>
    </div>
    <div class="map">
      <p class="title">Odwiedź nas</p>
      <br />
      pokój 23
      <br />
      ul. Wiśniowa 56
      <br />
      02-520 Warszawa
    </div>
    <div class="links">
      <p class="title">Zobacz media</p>
      <a href="https://facebook.wisniowasu.pl">
        <img
          src="/img/icons/icons8-facebook-50.png"
          alt="facebook"
          width="40"
        />
      </a>
      <a href="https://instagram.wisniowasu.pl">
        <img
          src="/img/icons/icons8-instagram-50.png"
          alt="instagram"
          width="40"
        />
      </a>
      <a href="https://discord.wisniowasu.pl">
        <img
          src="/img/icons/icons8-discord-new-logo-50.png"
          alt="discord"
          width="40"
        />
      </a>
    </div>
  </div>
  <iframe
    title="discord"
    class="discord slideable"
    src="https://discordapp.com/widget?id=497703565738115085&theme=light"
    width="350"
    height="500"
    allowtransparency={true}
    frameborder="0"
  />
</div>

<style lang="scss">
  #contact-container {
    display: flex;
    flex-wrap: wrap;
    justify-content: center;
  }

  .smallbox {
    margin: 20px;
    width: 100%;
    min-width: 220px;
    max-width: 350px;
    min-height: 460px;
    background-color: white;
    border-radius: 5px;
    overflow: hidden;
    box-shadow: 0 0 20px 0 rgba(0, 0, 0, 0.2);
    display: flex;
    flex-direction: column;
    flex-wrap: wrap;

    .title {
      margin: 0;
      text-transform: uppercase;
      font-weight: 700;
      font-size: 20px;
      font-family: "Raleway", sans-serif;
      color: rgba(0, 0, 0, 0.7);
    }

    .links {
      > a {
        display: inline-block;
        width: 40px;
        height: 40px;
        margin-top: 10px;
        filter: drop-shadow(0 0 2px rgba(0, 0, 0, 0.2));
        transition: all 0.1s ease-in-out;
      }

      @media (hover: hover) {
        > a:hover {
          filter: drop-shadow(0 0 4px rgba(0, 0, 0, 0.3));
        }
      }
    }

    .subtitle {
      margin: 5px 0 5px 0;
      text-transform: uppercase;
      font-weight: 500;
      font-size: 13px;
      color: rgba(0, 0, 0, 0.8);
    }

    & > div {
      margin: 20px;
    }
  }

  iframe.discord {
    min-width: 220px;
    height: 500px;
    margin: 20px;
    border-radius: 5px;
    overflow: hidden;
    box-shadow: 0 0 20px 0 rgba(0, 0, 0, 0.2);
  }
</style>
