<script lang="ts">
	import { melt } from "@melt-ui/svelte";
	import { getCtx } from "../ctx.js";
	import type { PrevButtonEvents, PrevButtonProps } from "../index.js";
	import { createDispatcher } from "$lib/internal/events.js";

	type $$Props = PrevButtonProps;
	type $$Events = PrevButtonEvents;

	export let asChild: $$Props["asChild"] = false;
	export let el: $$Props["el"] = undefined;

	const {
		elements: { prevButton },
		getCalendarAttrs,
	} = getCtx();

	const attrs = getCalendarAttrs("prev-button");

	$: builder = $prevButton;
	$: Object.assign(builder, attrs);

	const dispatch = createDispatcher();
</script>

{#if asChild}
	<slot {builder} />
{:else}
	<button bind:this={el} use:melt={builder} type="button" {...$$restProps} on:m-click={dispatch}>
		<slot {builder} />
	</button>
{/if}
