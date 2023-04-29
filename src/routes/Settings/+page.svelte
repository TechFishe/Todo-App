<script lang="ts">
	import { browser } from "$app/environment";

	let modal: any;

	function deleteList() {
		if (browser) {
			localStorage.removeItem("todo");
		}
		modal.close();
	}
</script>

<svelte:head>
	<title>Settings</title>
</svelte:head>

<header class="ml-4">
	<h1>Settings</h1>
</header>

<ul class="ml-8 mt-8">
	<li>
		<button
			on:click={() => modal.showModal()}
			class="flex items-center space-x-2 rounded-md border border-[#424651]/50 px-4 py-2 shadow-md transition-all delay-75 duration-200 ease-in hover:border-red-500 hover:text-red-500 hover:shadow-red-500/75">
			<svg
				xmlns="http://www.w3.org/2000/svg"
				fill="none"
				viewBox="0 0 24 24"
				stroke-width="1.5"
				stroke="currentColor"
				class="h-6 w-6">
				<path
					stroke-linecap="round"
					stroke-linejoin="round"
					d="M14.74 9l-.346 9m-4.788 0L9.26 9m9.968-3.21c.342.052.682.107 1.022.166m-1.022-.165L18.16 19.673a2.25 2.25 0 01-2.244 2.077H8.084a2.25 2.25 0 01-2.244-2.077L4.772 5.79m14.456 0a48.108 48.108 0 00-3.478-.397m-12 .562c.34-.059.68-.114 1.022-.165m0 0a48.11 48.11 0 013.478-.397m7.5 0v-.916c0-1.18-.91-2.164-2.09-2.201a51.964 51.964 0 00-3.32 0c-1.18.037-2.09 1.022-2.09 2.201v.916m7.5 0a48.667 48.667 0 00-7.5 0" />
			</svg>
			<span class="text-lg font-medium">Delete Lists</span>
		</button>
	</li>
</ul>

<dialog
	bind:this={modal}
	class="absolute rounded-lg border border-[#424651]/50 bg-transparent px-2 py-4 shadow-xl max-sm:w-5/6 sm:w-1/3">
	<header class="flex">
		<span class="border-b-2 border-[#424651]/[0.15] pl-2 pr-6 text-xl font-semibold"
			>Comfirm Pop-up</span>
		<!-- <button on:click={() => modal.close()}>
            <svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke-width="1.5" stroke="currentColor" class="w-6 h-6">
                <path stroke-linecap="round" stroke-linejoin="round" d="M6 18L18 6M6 6l12 12" />
            </svg>              
        </button> -->
	</header>
	<p class="my-2">
		Hey, we know things get hard, so we just wanted to check if you really wanted to delete your
		to-do list. This will completely remove it forever and is irreversible.
	</p>
	<section class="flex space-x-8">
		<button
			on:click={deleteList}
			class="flex-grow rounded-md border border-[#424651]/50 px-2 py-1 transition-all delay-75 duration-200 ease-in hover:border-green-500 hover:text-green-500 hover:shadow-md hover:shadow-green-500/75">
			Yes
		</button>
		<button
			on:click={() => modal.close()}
			class="flex-grow rounded-md border border-[#424651]/50 px-2 py-1 transition-all delay-75 duration-200 ease-in hover:border-red-500 hover:text-red-500 hover:shadow-md hover:shadow-red-500/75">
			No
		</button>
	</section>
</dialog>

<!-- <style>
    dialog button{
        @apply ;
    }
</style> -->
