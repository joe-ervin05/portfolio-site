<script lang="ts">
  import Stars from "./Stars.svelte";
  import Moon from "./Moon.svelte";
  import ShootingStar from "./ShootingStar.svelte";
</script>

<!--
  Space Background

  A decorative background featuring:
  - Twinkling stars that appear on page load
  - A moon in the top-right corner (desktop only)
  - A shooting star that periodically streaks across the screen
-->
<div class="space-background">
  <Stars />

  <!-- Moon: desktop only -->
  <div class="hidden md:block">
    <Moon />
  </div>

  <ShootingStar />
</div>

<style>
  .space-background {
    position: fixed;
    inset: 0;
    pointer-events: none;
    overflow: hidden;
    z-index: 0;
  }
</style>
