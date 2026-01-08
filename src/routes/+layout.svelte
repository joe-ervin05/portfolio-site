<script lang="ts">
  import "../app.css";
  import favicon from "$lib/assets/favicon.svg";
  import { SpaceBackground } from "$lib/components/space";

  let { children } = $props();
</script>

<svelte:head>
  {@html `<script>document.documentElement.classList.add('dark');</script>`}
  <link rel="icon" href={favicon} />
  <link rel="preconnect" href="https://fonts.googleapis.com" />
  <link
    rel="preconnect"
    href="https://fonts.gstatic.com"
    crossorigin="anonymous"
  />
  <link
    href="https://fonts.googleapis.com/css2?family=Space+Grotesk:wght@300..700&display=swap"
    rel="stylesheet"
  />
</svelte:head>

<SpaceBackground />

{@render children()}
