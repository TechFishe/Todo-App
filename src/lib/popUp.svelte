<script lang="ts">
	export let title: string;
	export let showPop: boolean, showXBtn: boolean;
	let popUp: any;

	$: if (popUp && showPop) popUp.showModal();

	export function hidePop() {
		popUp.close();
	}
</script>

<dialog
	bind:this={popUp}
	on:close={() => (showPop = false)}
	class="rounded-lg p-0 py-2 shadow-lg shadow-[#759FBC] max-sm:w-full sm:w-1/3">
	<header class="flex items-center border-b-2 border-[#424651]/50 px-4 py-1">
		<span class="flex-grow pr-4 font-mono text-3xl font-semibold tracking-wide">{title}</span>
		{#if showXBtn}
			<button
				on:click={() => popUp.close()}
				class="h-fit rounded-full p-1.5 transition-all duration-200 ease-in hover:bg-[#424651]/25 hover:shadow-md">
				<svg
					xmlns="http://www.w3.org/2000/svg"
					fill="none"
					viewBox="0 0 24 24"
					stroke-width="1.5"
					stroke="currentColor"
					class="h-6 w-6">
					<path stroke-linecap="round" stroke-linejoin="round" d="M6 18L18 6M6 6l12 12" />
				</svg>
			</button>
		{/if}
	</header>
	<slot />
</dialog>
