<script lang="ts">
  const starCount = 150;
  const stars = Array.from({ length: starCount }, (_, i) => ({
    id: i,
    x: Math.random() * 100,
    y: Math.random() * 100,
    size: Math.random() * 2 + 1,
    opacity: 0.3 + Math.random() * 0.4,
    delay: Math.random() * 3,
    duration: Math.random() * 2 + 2,
  }));
</script>

<div
  class="fixed inset-0 pointer-events-none overflow-hidden hidden dark:block"
>
  {#each stars as star}
    <div
      class="absolute rounded-full bg-white"
      style="
        left: {star.x}%;
        top: {star.y}%;
        width: {star.size}px;
        height: {star.size}px;
        opacity: {star.opacity};
        animation: twinkle {star.duration}s ease-in-out {star.delay}s infinite;
      "
    ></div>
  {/each}
</div>

<style>
  @keyframes twinkle {
    0%,
    100% {
      opacity: 0.3;
    }
    50% {
      opacity: 0.7;
    }
  }
</style>
