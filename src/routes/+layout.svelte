<script lang="ts">
  import { afterNavigate } from "$app/navigation";
  import { page } from "$app/stores";

  import "lazysizes";

  import "$lib/scss/main.scss";
  import Menu from "./Menu.svelte";
  import Footer from "./Footer.svelte";

  let currentPage: string;

  let isNavBtnBackgroundShown = false;
  let isLogoNotShown = true;

  afterNavigate(() => {
    currentPage = $page.route.id as string;

    window.addEventListener("scroll", () => {
      let scrollPosition = document.scrollingElement?.scrollTop as number;

      function isPageScrolledBelowHeader(scrollPosition: number): boolean {
        if (currentPage === "/")
          return scrollPosition / window.innerHeight > 0.7;
        else return scrollPosition > 170;
      }

      if (isPageScrolledBelowHeader(scrollPosition)) {
        isNavBtnBackgroundShown = true;
      } else if (isNavBtnBackgroundShown) {
        isNavBtnBackgroundShown = false;
      }
    });
  });
</script>

<Menu {isNavBtnBackgroundShown} {isLogoNotShown} {currentPage} />
<slot />
<Footer />
