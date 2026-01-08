<script lang="ts">
  interface Crater {
    cx: number;
    cy: number;
    r: number;
    fill: string;
  }

  const baseCraters: Crater[] = [
    { cx: 40, cy: 45, r: 12, fill: "#d0d0d0" },
    { cx: 70, cy: 35, r: 8, fill: "#c8c8c8" },
    { cx: 55, cy: 70, r: 10, fill: "#d4d4d4" },
    { cx: 80, cy: 65, r: 6, fill: "#cccccc" },
    { cx: 35, cy: 75, r: 5, fill: "#d0d0d0" },
  ];

  const innerCraterShadows: Crater[] = [
    { cx: 42, cy: 47, r: 6, fill: "#c0c0c0" },
    { cx: 71, cy: 36, r: 4, fill: "#b8b8b8" },
    { cx: 57, cy: 72, r: 5, fill: "#c4c4c4" },
  ];
</script>

<div class="moon-container">
  <svg width="120" height="120" viewBox="0 0 120 120" fill="none">
    <!-- Moon surface -->
    <circle cx="60" cy="60" r="50" fill="#e8e8e8" />

    <!-- Base craters -->
    {#each baseCraters as crater}
      <circle cx={crater.cx} cy={crater.cy} r={crater.r} fill={crater.fill} />
    {/each}

    <!-- Inner crater shadows for depth -->
    {#each innerCraterShadows as shadow}
      <circle cx={shadow.cx} cy={shadow.cy} r={shadow.r} fill={shadow.fill} />
    {/each}

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

<style>
  .moon-container {
    position: absolute;
    right: 5rem;
    top: 6rem;
    opacity: 0;
    animation: moon-appear 1.5s ease-out 1.5s forwards;
  }

  @keyframes moon-appear {
    from {
      opacity: 0;
      transform: scale(0.8);
    }
    to {
      opacity: 1;
      transform: scale(1);
    }
  }
</style>
