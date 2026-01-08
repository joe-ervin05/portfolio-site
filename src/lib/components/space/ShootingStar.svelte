<script lang="ts">
  // Shooting star travels from top-right to bottom-left
  // with the bright head leading and tail trailing behind
</script>

<div class="shooting-star"></div>

<style>
  .shooting-star {
    position: absolute;
    width: 80px;
    height: 2px;
    border-radius: 2px;

    /* Gradient: bright head on left, fading tail on right */
    background: linear-gradient(90deg, white, transparent);
    box-shadow: 0 0 6px 2px rgba(255, 255, 255, 0.3);

    /* Start off-screen to the right */
    top: 15%;
    right: -100px;
    opacity: 0;

    /* Animate every 10 seconds, starting after 4s delay */
    animation: shoot 10s ease-in-out 4s infinite;
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
    /* Stay hidden for the rest of the cycle */
    100% {
      right: 110%;
      top: 30%;
      opacity: 0;
    }
  }
</style>
