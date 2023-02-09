<script lang="ts">
  import { onMount } from "svelte";
  import { page } from "$app/stores";

  import "lazysizes";
  import "progressive-image.js";

  import "$lib/scss/main.scss";
  import Menu from "$lib/components/Menu.svelte";
  import Footer from "$lib/components/Footer.svelte";

  const currentPage = $page.route.id as string;
  let isNavBg = false;
  let isNoLogo = true;

  onMount(() => {
    window.onscroll = function () {
      var viewH = window.innerHeight;
      var scrollPosition = document.scrollingElement?.scrollTop as number;

      const isPageScrolledBelowHeader =
        currentPage === "/"
          ? scrollPosition / viewH > 0.7
          : scrollPosition > 170;

      if (isPageScrolledBelowHeader) {
        isNavBg = true;
      } else {
        if (isNavBg) {
          isNavBg = false;
        }
      }
    };
  });
</script>

<Menu {isNavBg} {isNoLogo} {currentPage} />
<slot />
<Footer />
