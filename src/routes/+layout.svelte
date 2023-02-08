<script lang="ts">
  import { onMount } from "svelte";
  import { page } from "$app/stores";

  import "lazysizes";
  import "progressive-image.js";

  import "../main.scss";
  import Menu from "$lib/components/Menu.svelte";
  import Footer from "$lib/components/Footer.svelte";

  const currentPage = $page.route.id as string;
  let isNavBg = false;
  let isNoLogo = true;

  onMount(() => {
    window.onscroll = function () {
      var viewH = window.innerHeight;
      var scrollPosition = document.scrollingElement?.scrollTop as number;
      var body = document.body;

      if (scrollPosition / viewH > 0.7) {
        isNavBg = true;
      } else {
        if (isNavBg) {
          isNavBg = false;
        }
      }
    };
  });
</script>

<svelte:head>
  <title>Wiśniowa SU | Samorząd Uczniowski</title>
</svelte:head>

<Menu {isNavBg} {isNoLogo} {currentPage} />
<slot />
<Footer />
