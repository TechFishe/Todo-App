<script lang="ts">
	import { page } from "$app/stores";
	import { onMount } from "svelte";
	import { browser } from "$app/environment";
	import { showDelMSG } from "$src/store";
	import PopUp from "$lib/popUp.svelte";

	let showDelPop = false,
		tempShowDelEver = false,
		showAddPop = false;
	let delPop: PopUp, addPop: PopUp;
	let inputTask = "";
	let currItem: number;

	let name = "",
		des = "",
		items: string[] = [],
		list: any;
	onMount(() => {
		if (browser) {
			let tempList: any = localStorage.getItem("lists");
			list = JSON.parse(tempList)[$page.params.id];
			name = list.name;
			des = list.des;
			for (let i = 0; i < list.items.length; i++) items[i] = list.items[i];
		}
	});

	function addItem() {
		showAddPop = false;
		addPop.hidePop();
		items = [...items, inputTask];
		inputTask = "";
		if (browser) {
			for (let i = 0; i < items.length; i++) list.items[i] = items[i];
			let tempList: any = localStorage.getItem("lists");
			let _tempList = JSON.parse(tempList);
			_tempList[$page.params.id] = list;
			localStorage.setItem("lists", JSON.stringify(_tempList));
		}
	}

	function deleteItem(fromPopUp: boolean) {
		if (fromPopUp) {
			showDelPop = false;
			delPop.hidePop();
			$showDelMSG = !tempShowDelEver;
		}
		items.splice(currItem, 1);
		items = items;
		if (browser) {
			list.items = items;
			let tempList: any = localStorage.getItem("lists");
			let _tempList = JSON.parse(tempList);
			_tempList[$page.params.id] = list;
			localStorage.setItem("lists", JSON.stringify(_tempList));
		}
	}
</script>

{#if name != ""}
	<header class="flex items-center pr-2">
		<div
			class="flex w-fit items-center justify-self-start border-b-2 border-LightGray/50 px-4 pb-2">
			<a
				href="/Lists"
				class="mr-2 h-fit rounded-full border border-OffWhite p-1.5 transition-all duration-200 ease-linear hover:border-LightGray/50 hover:text-LightBlue hover:shadow-md hover:shadow-LightBlue/75">
				<svg
					xmlns="http://www.w3.org/2000/svg"
					fill="none"
					viewBox="0 0 24 24"
					stroke-width="1.5"
					stroke="currentColor">
					<path
						stroke-linecap="round"
						stroke-linejoin="round"
						d="M10.5 19.5L3 12m0 0l7.5-7.5M3 12h18" />
				</svg>
			</a>
			<h1 class="h-fit border-l border-LightGray/25 pl-2">{name}</h1>
		</div>
		<div class="flex-grow" />
		<section class="flex items-center space-x-4 px-4">
			<button on:click={() => (showAddPop = true)}>
				<svg
					xmlns="http://www.w3.org/2000/svg"
					fill="none"
					viewBox="0 0 24 24"
					stroke-width="1.5"
					stroke="currentColor">
					<path stroke-linecap="round" stroke-linejoin="round" d="M12 4.5v15m7.5-7.5h-15" />
				</svg>
			</button>
			<button>
				<svg
					xmlns="http://www.w3.org/2000/svg"
					fill="none"
					viewBox="0 0 24 24"
					stroke-width="1.5"
					stroke="currentColor">
					<path
						stroke-linecap="round"
						stroke-linejoin="round"
						d="M6.72 13.829c-.24.03-.48.062-.72.096m.72-.096a42.415 42.415 0 0110.56 0m-10.56 0L6.34 18m10.94-4.171c.24.03.48.062.72.096m-.72-.096L17.66 18m0 0l.229 2.523a1.125 1.125 0 01-1.12 1.227H7.231c-.662 0-1.18-.568-1.12-1.227L6.34 18m11.318 0h1.091A2.25 2.25 0 0021 15.75V9.456c0-1.081-.768-2.015-1.837-2.175a48.055 48.055 0 00-1.913-.247M6.34 18H5.25A2.25 2.25 0 013 15.75V9.456c0-1.081.768-2.015 1.837-2.175a48.041 48.041 0 011.913-.247m10.5 0a48.536 48.536 0 00-10.5 0m10.5 0V3.375c0-.621-.504-1.125-1.125-1.125h-8.25c-.621 0-1.125.504-1.125 1.125v3.659M18 10.5h.008v.008H18V10.5zm-3 0h.008v.008H15V10.5z" />
				</svg>
			</button>
			<button>
				<svg
					xmlns="http://www.w3.org/2000/svg"
					fill="none"
					viewBox="0 0 24 24"
					stroke-width="1.5"
					stroke="currentColor">
					<path
						stroke-linecap="round"
						stroke-linejoin="round"
						d="M3.75 12h16.5m-16.5 3.75h16.5M3.75 19.5h16.5M5.625 4.5h12.75a1.875 1.875 0 010 3.75H5.625a1.875 1.875 0 010-3.75z" />
				</svg>
			</button>
		</section>
	</header>
	{#if items.length != 0}
		<ul class="space-y-2 p-2">
			{#each items as item, i}
				<li class="flex items-center rounded-md border border-LightGray/50 px-4 py-2">
					<svg
						xmlns="http://www.w3.org/2000/svg"
						fill="none"
						viewBox="0 0 24 24"
						stroke-width="1.5"
						stroke="#759FBC">
						<path stroke-linecap="round" stroke-linejoin="round" d="M18 12H6" />
					</svg>
					<span>{item}</span>
					<button class="hover:text-green-500">
						<svg
							xmlns="http://www.w3.org/2000/svg"
							fill="none"
							viewBox="0 0 24 24"
							stroke-width="1.5"
							stroke="currentColor">
							<path stroke-linecap="round" stroke-linejoin="round" d="M4.5 12.75l6 6 9-13.5" />
						</svg>
					</button>
					<button
						class="hover:text-red-500"
						on:click={() => {
							currItem = i;
							if ($showDelMSG) showDelPop = true;
							else deleteItem(false);
						}}>
						<svg
							xmlns="http://www.w3.org/2000/svg"
							fill="none"
							viewBox="0 0 24 24"
							stroke-width="1.5"
							stroke="currentColor">
							<path
								stroke-linecap="round"
								stroke-linejoin="round"
								d="M14.74 9l-.346 9m-4.788 0L9.26 9m9.968-3.21c.342.052.682.107 1.022.166m-1.022-.165L18.16 19.673a2.25 2.25 0 01-2.244 2.077H8.084a2.25 2.25 0 01-2.244-2.077L4.772 5.79m14.456 0a48.108 48.108 0 00-3.478-.397m-12 .562c.34-.059.68-.114 1.022-.165m0 0a48.11 48.11 0 013.478-.397m7.5 0v-.916c0-1.18-.91-2.164-2.09-2.201a51.964 51.964 0 00-3.32 0c-1.18.037-2.09 1.022-2.09 2.201v.916m7.5 0a48.667 48.667 0 00-7.5 0" />
						</svg>
					</button>
				</li>
			{/each}
		</ul>
	{:else}
		<p class="px-4 pt-4 text-center text-lg font-medium tracking-wide">
			It looks like you don't have any tasks. Click the "<span class="text-LightBlue">+</span>"
			button to add one.
		</p>
	{/if}
{/if}

<PopUp bind:showPop={showDelPop} bind:this={delPop} title="Confirm Delete" showXBtn={false}>
	<section class="px-4 py-1">
		<p class="indent-4">
			Woah there. Are you sure you really want to delete this task before completing it?
		</p>
		<p>Note: Once tasks are deleted, they can <span class="text-red-500">NEVER</span> come back</p>
	</section>
	<section class="flex w-full justify-evenly space-x-4 px-4 py-1">
		<button
			on:click={() => {
				showDelPop = false;
				delPop.hidePop();
				$showDelMSG = !tempShowDelEver;
			}}
			class="flex-grow rounded-md border border-LightGray px-2 py-1 transition-all duration-200 ease-in hover:border-green-500 hover:text-green-500 hover:shadow-md hover:shadow-green-500/75">
			Keep it
		</button>
		<button
			on:click={() => deleteItem(true)}
			class="flex-grow rounded-md border border-LightGray px-2 py-1 transition-all duration-200 ease-in hover:border-red-500 hover:text-red-500 hover:shadow-md hover:shadow-red-500/75">
			Delete it
		</button>
	</section>
	<div class="px-4 py-1">
		<input type="checkbox" bind:checked={tempShowDelEver} id="check" />
		<label for="check"
			>Never show me this again (This <span class="text-green-500">CAN</span> be changed)</label>
	</div>
</PopUp>

<PopUp bind:showPop={showAddPop} bind:this={addPop} title="New Task" showXBtn={true}>
	<section class="w-full flex-row space-y-2 px-4 py-1">
		<input
			type="text"
			id="text1"
			placeholder="Task name"
			bind:value={inputTask}
			class="w-full rounded-md border border-LightGray/50 bg-OffWhite px-2 py-1 transition-all duration-200 ease-in placeholder:italic hover:shadow-md focus:caret-LightBlue focus:shadow-md" />
		<div class="flex w-full justify-center">
			<button
				on:click={addItem}
				class="rounded-md border border-LightGray px-2 py-1 transition-all duration-200 ease-in hover:border-green-500 hover:text-green-500 hover:shadow-md hover:shadow-green-500/75">
				Submit
			</button>
		</div>
	</section>
</PopUp>

<style>
	header svg {
		width: 2rem;
		height: 2rem;
	}
	header section button {
		padding: 0.375rem;
		border-width: 1px;
		border-color: #fff2f1;
		border-radius: 100%;
		@apply transition-all duration-200 ease-in;
	}
	header section button:hover {
		color: #759fbc;
		border-color: rgb(66 70 81 / 0.5);
		@apply shadow-md shadow-LightBlue/75;
	}
	li button {
		margin: 0.25rem;
		@apply transition-colors duration-200 ease-linear;
	}
	li svg {
		width: 1.5rem;
		height: 1.5rem;
	}
	li span {
		padding: 0 1rem 0 0.5rem;
		font-size: 1.125rem;
		line-height: 1.75rem;
		flex-grow: 1;
	}
</style>
