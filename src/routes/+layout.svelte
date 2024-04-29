<script lang="ts">
  import Navbar from "$lib/components/navbar.svelte";
  import Footer from "$lib/components/footer.svelte";
  import "../tail.css"; 

  import { onMount } from "svelte";

  function placeFooter() {
    const footer: HTMLElement | null = document.querySelector('.footer-container');
    const pageContent: HTMLElement | null = document.querySelector('.page-content');
    if (!footer || !pageContent) return;
    const footerOffset = window.innerHeight * 0.275;
    const contentHeight = pageContent.offsetHeight;
    footer.style.top = `${footerOffset + contentHeight}px`;
  }
  onMount(() => {
    placeFooter();
    // also replace on resize
    window.addEventListener('resize', placeFooter);
  });
</script>

<Navbar github="https://avatars.githubusercontent.com/u/104609738?v=4" />
<div class="page-content">
  <slot />
</div>
  <Footer />

<style>
  .page-content {
    position: absolute;
    top: 20%;
    width: 70%;
   /* min-height: 80vh; */
    margin-left: 15%;
    margin-right: 15%;
    display: flex;
    flex-flow: column;
    align-items: center;
  }
  @media only screen and (max-width: 600px) {
    .page-content {
      width: 100%;
      margin-left: 0;
      margin-right: 0;
    }
  }
</style>