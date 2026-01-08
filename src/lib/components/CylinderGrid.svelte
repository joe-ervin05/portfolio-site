<script lang="ts">
  const verticalLineCount = 21;
  const horizontalLineCount = 25;
  const lineDuration = 2; // seconds
  const staggerDelay = 0.05; // seconds between each line
  const horizontalStartDelay = 0.3; // seconds before horizontal lines start

  function getVerticalLinePath(index: number): string {
    const x = index * 5;
    const curveOffset = index < 10 ? (10 - index) * 1.5 : (index - 10) * -1.5;
    return `M ${x} 0 Q ${x + curveOffset} 50 ${x} 100`;
  }

  function getHorizontalLinePath(index: number): string {
    const y = index * 4;
    const curveOffset = index < 12 ? (12 - index) * 1.5 : (index - 12) * 1.5;
    return `M 0 ${y} Q 50 ${y + curveOffset} 100 ${y}`;
  }

  function getVerticalLineDelay(index: number): string {
    return `${index * staggerDelay}s`;
  }

  function getHorizontalLineDelay(index: number): string {
    return `${horizontalStartDelay + index * staggerDelay}s`;
  }
</script>

<div
  class="absolute inset-0 pointer-events-none flex items-center justify-center"
>
  <svg
    class="w-[120%] h-[120%] text-primary opacity-[0.12] animate-[pulse-grid_20s_ease-in-out_infinite]"
    viewBox="0 0 100 100"
    preserveAspectRatio="none"
    xmlns="http://www.w3.org/2000/svg"
  >
    <!-- Curved vertical lines -->
    {#each Array(verticalLineCount) as _, i}
      <path
        d={getVerticalLinePath(i)}
        fill="none"
        stroke="currentColor"
        stroke-width="0.15"
        class="animate-[draw-line_{lineDuration}s_ease-out_forwards]"
        style="
          stroke-dasharray: 150;
          stroke-dashoffset: 150;
          animation: draw-line {lineDuration}s ease-out forwards;
          animation-delay: {getVerticalLineDelay(i)};
        "
      />
    {/each}

    <!-- Curved horizontal lines -->
    {#each Array(horizontalLineCount) as _, i}
      <path
        d={getHorizontalLinePath(i)}
        fill="none"
        stroke="currentColor"
        stroke-width="0.15"
        style="
          stroke-dasharray: 150;
          stroke-dashoffset: 150;
          animation: draw-line {lineDuration}s ease-out forwards;
          animation-delay: {getHorizontalLineDelay(i)};
        "
      />
    {/each}
  </svg>
</div>
