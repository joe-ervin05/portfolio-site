<script lang="ts" module>
	import { cn, type WithElementRef } from "$lib/utils.js";
	import type { HTMLAnchorAttributes, HTMLButtonAttributes } from "svelte/elements";
	import { type VariantProps, tv } from "tailwind-variants";

	export const buttonVariants = tv({
		base: "inline-flex shrink-0 items-center justify-center gap-2 rounded-none text-sm font-semibold uppercase tracking-wide whitespace-nowrap transition-all outline-none border-2 disabled:pointer-events-none disabled:opacity-50 aria-disabled:pointer-events-none aria-disabled:opacity-50 [&_svg]:pointer-events-none [&_svg]:shrink-0 [&_svg:not([class*='size-'])]:size-4",
		variants: {
			variant: {
				default: "bg-primary text-primary-foreground border-primary shadow-[4px_4px_0px_0px] shadow-primary/40 hover:translate-x-[2px] hover:translate-y-[2px] hover:shadow-[2px_2px_0px_0px] hover:shadow-primary/40 active:translate-x-[4px] active:translate-y-[4px] active:shadow-none",
				destructive:
					"bg-destructive text-white border-destructive shadow-[4px_4px_0px_0px] shadow-destructive/40 hover:translate-x-[2px] hover:translate-y-[2px] hover:shadow-[2px_2px_0px_0px] hover:shadow-destructive/40 active:translate-x-[4px] active:translate-y-[4px] active:shadow-none",
				outline:
					"bg-background text-foreground border-foreground shadow-[4px_4px_0px_0px] shadow-foreground/30 hover:translate-x-[2px] hover:translate-y-[2px] hover:shadow-[2px_2px_0px_0px] hover:shadow-foreground/30 active:translate-x-[4px] active:translate-y-[4px] active:shadow-none",
				secondary: "bg-secondary text-secondary-foreground border-border shadow-[4px_4px_0px_0px] shadow-border hover:translate-x-[2px] hover:translate-y-[2px] hover:shadow-[2px_2px_0px_0px] hover:shadow-border active:translate-x-[4px] active:translate-y-[4px] active:shadow-none",
				ghost: "border-transparent hover:bg-accent hover:text-accent-foreground",
				link: "border-transparent text-foreground underline-offset-4 hover:underline",
			},
			size: {
				default: "h-10 px-5 py-2 has-[>svg]:px-4",
				sm: "h-9 gap-1.5 px-4 has-[>svg]:px-3",
				lg: "h-11 px-7 has-[>svg]:px-5",
				icon: "size-10",
				"icon-sm": "size-9",
				"icon-lg": "size-11",
			},
		},
		defaultVariants: {
			variant: "default",
			size: "default",
		},
	});

	export type ButtonVariant = VariantProps<typeof buttonVariants>["variant"];
	export type ButtonSize = VariantProps<typeof buttonVariants>["size"];

	export type ButtonProps = WithElementRef<HTMLButtonAttributes> &
		WithElementRef<HTMLAnchorAttributes> & {
			variant?: ButtonVariant;
			size?: ButtonSize;
		};
</script>

<script lang="ts">
	let {
		class: className,
		variant = "default",
		size = "default",
		ref = $bindable(null),
		href = undefined,
		type = "button",
		disabled,
		children,
		...restProps
	}: ButtonProps = $props();
</script>

{#if href}
	<a
		bind:this={ref}
		data-slot="button"
		class={cn(buttonVariants({ variant, size }), className)}
		href={disabled ? undefined : href}
		aria-disabled={disabled}
		role={disabled ? "link" : undefined}
		tabindex={disabled ? -1 : undefined}
		{...restProps}
	>
		{@render children?.()}
	</a>
{:else}
	<button
		bind:this={ref}
		data-slot="button"
		class={cn(buttonVariants({ variant, size }), className)}
		{type}
		{disabled}
		{...restProps}
	>
		{@render children?.()}
	</button>
{/if}
