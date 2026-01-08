<script lang="ts">
  import { Sun, Moon } from "@lucide/svelte";
  import { Button } from "$lib/components/ui/button";

  let isDark = $state(false);

  $effect(() => {
    // Check for stored preference or system preference
    const stored = localStorage.getItem("theme");
    if (stored) {
      isDark = stored === "dark";
    } else {
      isDark = window.matchMedia("(prefers-color-scheme: dark)").matches;
    }
    updateTheme();
  });

  function updateTheme() {
    if (isDark) {
      document.documentElement.classList.add("dark");
    } else {
      document.documentElement.classList.remove("dark");
    }
  }

  function toggle() {
    isDark = !isDark;
    localStorage.setItem("theme", isDark ? "dark" : "light");
    updateTheme();
  }
</script>

<Button
  variant="outline"
  size="icon"
  onclick={toggle}
  aria-label={isDark ? "Switch to light mode" : "Switch to dark mode"}
>
  {#if isDark}
    <Sun class="h-5 w-5" />
  {:else}
    <Moon class="h-5 w-5" />
  {/if}
</Button>
