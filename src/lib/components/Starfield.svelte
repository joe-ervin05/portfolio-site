<script lang="ts">
  const starCount = 150;

  const stars = new Array(starCount).map((_, i) => ({
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

<div
  class="fixed inset-0 pointer-events-none overflow-hidden hidden dark:block"
>
  <!-- Stars -->
  {#each stars as star}
    <div
      class="star absolute rounded-full bg-white"
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

  <!-- Moon (desktop only) -->
  <div class="moon-container absolute right-20 top-24 hidden md:block">
    <svg width="120" height="120" viewBox="0 0 120 120" fill="none">
      <!-- Moon body -->
      <circle cx="60" cy="60" r="50" fill="#e8e8e8" />

      <!-- Craters -->
      <circle cx="40" cy="45" r="12" fill="#d0d0d0" />
      <circle cx="70" cy="35" r="8" fill="#c8c8c8" />
      <circle cx="55" cy="70" r="10" fill="#d4d4d4" />
      <circle cx="80" cy="65" r="6" fill="#cccccc" />
      <circle cx="35" cy="75" r="5" fill="#d0d0d0" />

      <!-- Inner crater shadows -->
      <circle cx="42" cy="47" r="6" fill="#c0c0c0" />
      <circle cx="71" cy="36" r="4" fill="#b8b8b8" />
      <circle cx="57" cy="72" r="5" fill="#c4c4c4" />

      <!-- Atmosphere glow -->
      <circle
        cx="60"
        cy="60"
        r="52"
        fill="none"
        stroke="rgba(200, 210, 255, 0.3)"
        stroke-width="6"
      />
    </svg>
  </div>

  <!-- Shooting star -->
  <div class="shooting-star"></div>
</div>

<style>
  .star {
    opacity: 0;
    animation:
      appear 0.8s ease-out var(--appear-delay) forwards,
      twinkle var(--twinkle-duration) ease-in-out var(--twinkle-delay) infinite;
  }

  @keyframes appear {
    0% {
      opacity: 0;
      transform: scale(0);
    }
    100% {
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

  /* Moon */
  .moon-container {
    opacity: 0;
    animation: moon-appear 1.5s ease-out 1.5s forwards;
  }

  @keyframes moon-appear {
    0% {
      opacity: 0;
      transform: scale(0.8);
    }
    100% {
      opacity: 1;
      transform: scale(1);
    }
  }

  /* Shooting star */
  .shooting-star {
    position: absolute;
    width: 80px;
    height: 2px;
    background: linear-gradient(90deg, white, transparent);
    top: 15%;
    right: -100px;
    opacity: 0;
    animation: shoot 10s ease-in-out 4s infinite;
    border-radius: 2px;
    box-shadow: 0 0 6px 2px rgba(255, 255, 255, 0.3);
  }

  @keyframes shoot {
    0% {
      right: -100px;
      top: 8%;
      opacity: 0;
      transform: rotate(-25deg);
    }
    2% {
      opacity: 1;
    }
    12% {
      right: 110%;
      top: 30%;
      opacity: 0;
    }
    100% {
      right: 110%;
      top: 30%;
      opacity: 0;
    }
  }
</style>
