<script lang="ts">
	import { browser } from "$app/environment";
	import { onMount } from "svelte";

	let todo: string[] = [];
	let input = "";

	onMount(() => {
		if (browser) {
			let storedTodo = localStorage.getItem("todo");
			if (storedTodo != null) {
				todo = JSON.parse(storedTodo);
			}
		}
	});

	function addItem() {
		todo = [...todo, input];
		input = "";
		if (browser) {
			localStorage.setItem("todo", JSON.stringify(todo));
		}
	}

	function deleteItem(i: number) {
		todo.splice(i, 1);
		todo = todo;
		if (browser) {
			localStorage.setItem("todo", JSON.stringify(todo));
		}
	}
</script>

<svelte:head>
    <title>To-Do List</title>
</svelte:head>

<header class="ml-4">
	<h1>To-do List</h1>
</header>
<ul
	class:hidden={todo.length === 0}
	class="mt-8 space-y-2 rounded-lg px-2 py-1 shadow-md max-sm:mx-8 sm:ml-8 sm:w-1/4">
	{#each todo as item, i}
		<li class="flex items-center rounded-md border border-[#424651]/25 px-4 py-2">
			<svg
				xmlns="http://www.w3.org/2000/svg"
				fill="none"
				viewBox="0 0 24 24"
				stroke-width="1.5"
				stroke="#759FBC"
				class="h-6 w-6">
				<path stroke-linecap="round" stroke-linejoin="round" d="M18 12H6" />
			</svg>
			<span class="flex-grow pl-2 pr-4 text-lg">{item}</span>
			<button class="m-1 transition-colors duration-200 ease-linear hover:text-yellow-500">
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
						d="M3 3v1.5M3 21v-6m0 0l2.77-.693a9 9 0 016.208.682l.108.054a9 9 0 006.086.71l3.114-.732a48.524 48.524 0 01-.005-10.499l-3.11.732a9 9 0 01-6.085-.711l-.108-.054a9 9 0 00-6.208-.682L3 4.5M3 15V4.5" />
				</svg>
			</button>
			<button
				class="m-1 transition-colors duration-200 ease-linear hover:text-red-500"
				on:click={() => deleteItem(i)}>
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
			</button>
			<!-- <button class="hover:text-[#759FBC] m-1 transition-colors duration-200 ease-linear">
                <svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke-width="1.5" stroke="currentColor" class="w-6 h-6">
                    <path stroke-linecap="round" stroke-linejoin="round" d="M6.75 12a.75.75 0 11-1.5 0 .75.75 0 011.5 0zM12.75 12a.75.75 0 11-1.5 0 .75.75 0 011.5 0zM18.75 12a.75.75 0 11-1.5 0 .75.75 0 011.5 0z" />
                </svg>
            </button> -->
		</li>
	{/each}
</ul>
<section class="absolute bottom-4 flex w-full px-4">
	<input
		type="text"
		bind:value={input}
		placeholder="Input task name"
		class="flex-grow rounded-l-lg border border-r-0 border-[#424651]/50 bg-transparent px-2 py-1 text-lg outline-0 placeholder:italic" />
	<button
		on:click={addItem}
		class="rounded-r-lg border border-l-0 border-[#424651]/50 px-2 py-1 transition-colors duration-200 ease-linear hover:text-[#759FBC]">
		<svg
			xmlns="http://www.w3.org/2000/svg"
			fill="none"
			viewBox="0 0 24 24"
			stroke-width="1.5"
			stroke="currentColor"
			class="h-8 w-8 -rotate-90">
			<path
				stroke-linecap="round"
				stroke-linejoin="round"
				d="M6 12L3.269 3.126A59.768 59.768 0 0121.485 12 59.77 59.77 0 013.27 20.876L5.999 12zm0 0h7.5" />
		</svg>
	</button>
</section>
