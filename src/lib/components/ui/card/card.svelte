<script lang="ts">
  import type { HTMLAttributes } from "svelte/elements";
  import { cn, type WithElementRef } from "$lib/utils.js";

  let {
    ref = $bindable(null),
    class: className,
    children,
    ...restProps
  }: WithElementRef<HTMLAttributes<HTMLDivElement>> = $props();
</script>

<div
  bind:this={ref}
  data-slot="card"
  class={cn(
    "bg-card/70 text-card-foreground flex flex-col gap-6 rounded-none border-2 border-foreground/20 py-6 shadow-[6px_6px_0px_0px] shadow-foreground/20 relative z-10",
    className
  )}
  {...restProps}
>
  {@render children?.()}
</div>
