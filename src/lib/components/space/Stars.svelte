<script lang="ts">
  const STAR_COUNT = 150;

  interface Star {
    id: number;
    x: number;
    y: number;
    size: number;
    opacity: number;
    appearDelay: number;
    twinkleDelay: number;
    twinkleDuration: number;
  }

  const stars: Star[] = Array.from({ length: STAR_COUNT }, (_, i) => ({
    id: i,
    x: Math.random() * 100,
    y: Math.random() * 100,
    size: Math.random() * 2 + 1,
    opacity: 0.3 + Math.random() * 0.4,
    appearDelay: Math.random() * 1.5,
    twinkleDelay: 2 + Math.random() * 3,
    twinkleDuration: Math.random() * 2 + 2,
  }));
</script>

{#each stars as star (star.id)}
  <div
    class="star"
    style="
      left: {star.x}%;
      top: {star.y}%;
      width: {star.size}px;
      height: {star.size}px;
      --final-opacity: {star.opacity};
      --appear-delay: {star.appearDelay}s;
      --twinkle-delay: {star.twinkleDelay}s;
      --twinkle-duration: {star.twinkleDuration}s;
    "
  ></div>
{/each}

<style>
  .star {
    position: absolute;
    border-radius: 50%;
    background-color: white;
    opacity: 0;
    animation:
      appear 0.8s ease-out var(--appear-delay) forwards,
      twinkle var(--twinkle-duration) ease-in-out var(--twinkle-delay) infinite;
  }

  @keyframes appear {
    from {
      opacity: 0;
      transform: scale(0);
    }
    to {
      opacity: var(--final-opacity);
      transform: scale(1);
    }
  }

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
