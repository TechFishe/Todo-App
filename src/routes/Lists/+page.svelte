<script lang="ts">
	import { browser } from "$app/environment";
	import { onMount } from "svelte";

	let listCheck:any, lists:any = [];
	let showInput:boolean = false;
	let inputName:string = "", inputDes:string = "";
	onMount(() => {
		if(browser){
			listCheck = localStorage.getItem("lists");
			if(listCheck != null)
				lists = JSON.parse(listCheck);
		}
	});

	function addList(){
		showInput = false;
		lists = [...lists, {
			"name": inputName,
			"des": inputDes,
			"items": []
		}];
		if(browser)
			localStorage.setItem("lists", JSON.stringify(lists));
		inputName = "";
		inputDes = ""
	}

	function delteArray(i:number){
		lists.splice(i, 1);
		lists = lists;
		if(browser)
			localStorage.setItem("lists", JSON.stringify(lists));
	}
</script>

<svelte:head>
	<title>Lists</title>
</svelte:head>

<header class="flex items-center mb-4">
	<h1 class="px-4 border-b-2 border-[#424651]/50 w-fit">Lists</h1>
	<div class="flex-grow" />
    <section class="flex px-4 space-x-4 items-center">
        <button on:click={() => showInput = true}>
            <svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke-width="1.5" stroke="currentColor">
                <path stroke-linecap="round" stroke-linejoin="round" d="M12 4.5v15m7.5-7.5h-15" />
            </svg>                         
        </button>
        <!-- <button>
            <svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke-width="1.5" stroke="currentColor">
                <path stroke-linecap="round" stroke-linejoin="round" d="M6.72 13.829c-.24.03-.48.062-.72.096m.72-.096a42.415 42.415 0 0110.56 0m-10.56 0L6.34 18m10.94-4.171c.24.03.48.062.72.096m-.72-.096L17.66 18m0 0l.229 2.523a1.125 1.125 0 01-1.12 1.227H7.231c-.662 0-1.18-.568-1.12-1.227L6.34 18m11.318 0h1.091A2.25 2.25 0 0021 15.75V9.456c0-1.081-.768-2.015-1.837-2.175a48.055 48.055 0 00-1.913-.247M6.34 18H5.25A2.25 2.25 0 013 15.75V9.456c0-1.081.768-2.015 1.837-2.175a48.041 48.041 0 011.913-.247m10.5 0a48.536 48.536 0 00-10.5 0m10.5 0V3.375c0-.621-.504-1.125-1.125-1.125h-8.25c-.621 0-1.125.504-1.125 1.125v3.659M18 10.5h.008v.008H18V10.5zm-3 0h.008v.008H15V10.5z" />
            </svg>              
        </button>
        <button>
            <svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke-width="1.5" stroke="currentColor">
                <path stroke-linecap="round" stroke-linejoin="round" d="M3.75 12h16.5m-16.5 3.75h16.5M3.75 19.5h16.5M5.625 4.5h12.75a1.875 1.875 0 010 3.75H5.625a1.875 1.875 0 010-3.75z" />
            </svg>                       
        </button> -->
    </section>
</header>
{#if lists.lenght != 0}
	<section class="grid max-sm:grid-cols-1 sm:grid-cols-4 gap-4 px-4">
		{#each lists as list, i}
			<article class="rounded-lg shadow-lg hover:shadow-[#759FBC] transition-shadow duration-300 ease-in px-4 py-2">
				<div class="border-b border-[#424651]/50 py-1 items-center flex space-x-2">
					<h2 class="text-ellipsis w-full">{list.name}</h2>
					<section class="flex space-x-2">
						<a href="Lists/{i}" class="w-fit rounded-full p-1 hover:text-[#759FBC] transition-all duration-200 ease-in">
							<svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke-width="1.5" stroke="currentColor" class="w-6 h-6">
								<path stroke-linecap="round" stroke-linejoin="round" d="M13.5 6H5.25A2.25 2.25 0 003 8.25v10.5A2.25 2.25 0 005.25 21h10.5A2.25 2.25 0 0018 18.75V10.5m-10.5 6L21 3m0 0h-5.25M21 3v5.25" />
							</svg>						  
						</a>
						<button on:click={() => delteArray(i)} class="w-fit rounded-full p-1 hover:text-red-500 transition-all duration-200 ease-in">
							<svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke-width="1.5" stroke="currentColor" class="w-6 h-6">
								<path stroke-linecap="round" stroke-linejoin="round" d="M14.74 9l-.346 9m-4.788 0L9.26 9m9.968-3.21c.342.052.682.107 1.022.166m-1.022-.165L18.16 19.673a2.25 2.25 0 01-2.244 2.077H8.084a2.25 2.25 0 01-2.244-2.077L4.772 5.79m14.456 0a48.108 48.108 0 00-3.478-.397m-12 .562c.34-.059.68-.114 1.022-.165m0 0a48.11 48.11 0 013.478-.397m7.5 0v-.916c0-1.18-.91-2.164-2.09-2.201a51.964 51.964 0 00-3.32 0c-1.18.037-2.09 1.022-2.09 2.201v.916m7.5 0a48.667 48.667 0 00-7.5 0" />
							</svg>						  
						</button>
					</section>
				</div>
				<p class="py-1">{list.des}</p>
			</article>
		{/each}
	</section>
	{:else}
		<p class="text-lg text-center tracking-wide font-medium">It looks like you don't have any lists. Click the "+" button to add one.</p>
{/if}

{#if showInput}
	<section class="absolute bottom-4 flex w-full px-4">
		<input
			type="text"
			bind:value={inputName}
			placeholder="Input task name"
			class="flex-grow rounded-l-lg border border-r-0 border-[#424651]/50 bg-transparent px-2 py-1 text-lg outline-0 placeholder:italic" />
		<button
			on:click={addList}
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
{/if}

<style>
	header svg{
		width: 2rem;
		height: 2rem;
	}
	header button{
        padding: 0.375rem;
        border-width: 1px;
		border-color: #fff2f1;
		border-radius: 100%;
        @apply transition-all duration-200 ease-in;
    }
    header button:hover{
        color: #759fbc;
		border-color: rgb(66 70 81 / 0.5);
        @apply shadow-md shadow-[#759FBC]/75;
    }
</style>
