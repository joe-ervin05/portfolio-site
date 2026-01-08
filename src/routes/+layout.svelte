<script lang="ts">
  import "../app.css";
  import favicon from "$lib/assets/favicon.svg";
  import ThemeToggle from "$lib/components/ThemeToggle.svelte";

  let { children } = $props();
</script>

<svelte:head>
  {@html `<script>
    (function() {
      const stored = localStorage.getItem('theme');
      const prefersDark = window.matchMedia('(prefers-color-scheme: dark)').matches;
      if (stored === 'dark' || (!stored && prefersDark)) {
        document.documentElement.classList.add('dark');
      }
    })();
  </script>`}
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

<div class="fixed top-6 right-6 z-50">
  <ThemeToggle />
</div>

{@render children()}
