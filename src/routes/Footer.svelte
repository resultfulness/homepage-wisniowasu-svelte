<script lang="ts">
  import { socials } from "$lib/content/footer";
</script>

<footer>
  <p class="poweredby">powered by</p>
  <a href="/" class="logo">
    <img src="/img/logos/logo_title.png" alt="logo Wiśniowa" width="300" />
  </a>
  <div class="icons">
    {#each socials as { identifier, title, href, iconSrc }}
      <a {href} class={identifier} {title} target="_blank" rel="noreferrer">
        <img src={iconSrc} alt={identifier} width="32" />
      </a>
    {/each}
  </div>
  <p>
    Made by <a
      target="_blank"
      href="https://github.com/resultfulness"
      rel="noreferrer">Alicja Rosiak</a
    >
    | Source code on
    <a
      target="_blank"
      href="https://github.com/resultfulness/homepage-wisniowasu-svelte"
      rel="noreferrer">GitHub</a
    >
  </p>
  <p>
    Original design by <a
      target="_blank"
      href="https://github.com/fastfend"
      rel="noreferrer">Piotr Stadnicki</a
    >
    | Source code on
    <a
      target="_blank"
      href="https://github.com/fastfend/homepage-wisniowasu"
      rel="noreferrer">GitHub</a
    >
  </p>
  <p>
    Ikony wykorzystane z <a
      target="_blank"
      rel="noreferrer"
      href="https://icons8.com">Icons8</a
    >
  </p>
  <p>wersja 0.1</p>
</footer>

<style lang="scss">
  footer {
    display: flex;
    justify-content: center;
    align-content: center;
    align-items: center;
    flex-direction: column;
    flex-wrap: nowrap;
    margin: 80px 0 0 0;
    padding-bottom: 20px;
    background-color: whitesmoke;
    box-shadow: 0 0 20px 20px whitesmoke;

    .logo {
      height: 60px;
      width: 300px;
      filter: grayscale(1);
      opacity: 0.6;
      margin: 20px;
      margin-bottom: 40px;
      transition: opacity 0.2s ease-in-out;
    }

    .logo:hover {
      opacity: 1;
    }

    div.icons {
      width: 100%;
      margin-bottom: 10px;
      height: 40px;
      display: flex;
      justify-content: center;
      align-content: center;
      align-items: center;

      a {
        margin: 5px;
        display: block;
        width: 32px;
        height: 32px;
        filter: grayscale(1);
        transition: filter 0.06s ease-in-out;
      }

      a:hover {
        filter: grayscale(0);
      }
    }

    p {
      margin: 3px;
      color: rgba(0, 0, 0, 0.4);
      text-align: center;

      a {
        color: rgba(0, 0, 0, 0.4);
        font-weight: bold;
        text-decoration: none;
      }

      a:hover {
        color: rgba(0, 0, 0, 0.8);
      }
    }

    p.poweredby {
      margin-bottom: -10px;
    }
  }
</style>
