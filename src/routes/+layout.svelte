<script>
	import "../app.css";
	import { page } from "$app/stores";

	let menuOpen = false;
</script>

<header
	class:max-sm:rounded-br-xl={!menuOpen}
	class="px-4 py-2 shadow-xl sm:flex sm:w-screen sm:rounded-bl-xl">
	<h1 class="w-2/3 text-6xl font-extrabold tracking-wider antialiased max-sm:hidden">To-do App</h1>
	<nav class="sm:w-1/3">
		<section class="flex items-center divide-x-[1px] divide-[#424651]/[0.15]">
			<div>
				<a href="/">
					<svg
						xmlns="http://www.w3.org/2000/svg"
						fill="none"
						viewBox="0 0 24 24"
						stroke-width="1.5"
						stroke="currentColor">
						<path
							stroke-linecap="round"
							stroke-linejoin="round"
							d="M2.25 12l8.954-8.955c.44-.439 1.152-.439 1.591 0L21.75 12M4.5 9.75v10.125c0 .621.504 1.125 1.125 1.125H9.75v-4.875c0-.621.504-1.125 1.125-1.125h2.25c.621 0 1.125.504 1.125 1.125V21h4.125c.621 0 1.125-.504 1.125-1.125V9.75M8.25 21h8.25" />
					</svg>
				</a>
			</div>
			<div>
				<a href="/Lists">
					<svg
						xmlns="http://www.w3.org/2000/svg"
						fill="none"
						viewBox="0 0 24 24"
						stroke-width="1.5"
						stroke="currentColor">
						<path
							stroke-linecap="round"
							stroke-linejoin="round"
							d={$page.route.id === "/Lists" || $page.route.id === "/Lists/[name]"
								? "M3.75 9.776c.112-.017.227-.026.344-.026h15.812c.117 0 .232.009.344.026m-16.5 0a2.25 2.25 0 00-1.883 2.542l.857 6a2.25 2.25 0 002.227 1.932H19.05a2.25 2.25 0 002.227-1.932l.857-6a2.25 2.25 0 00-1.883-2.542m-16.5 0V6A2.25 2.25 0 016 3.75h3.879a1.5 1.5 0 011.06.44l2.122 2.12a1.5 1.5 0 001.06.44H18A2.25 2.25 0 0120.25 9v.776"
								: "M2.25 12.75V12A2.25 2.25 0 014.5 9.75h15A2.25 2.25 0 0121.75 12v.75m-8.69-6.44l-2.12-2.12a1.5 1.5 0 00-1.061-.44H4.5A2.25 2.25 0 002.25 6v12a2.25 2.25 0 002.25 2.25h15A2.25 2.25 0 0021.75 18V9a2.25 2.25 0 00-2.25-2.25h-5.379a1.5 1.5 0 01-1.06-.44z"} />
					</svg>
				</a>
			</div>
			<div>
				<button on:click={() => (menuOpen = !menuOpen)}>
					<svg
						xmlns="http://www.w3.org/2000/svg"
						fill="none"
						viewBox="0 0 24 24"
						stroke-width="1.5"
						stroke="currentColor">
						<path
							stroke-linecap="round"
							stroke-linejoin="round"
							d="M3.75 6.75h16.5M3.75 12h16.5M12 17.25h8.25" />
					</svg>
				</button>
			</div>
		</section>
		<!-- {#if menuOpen}
			<aside
				class="absolute border-t-2 border-[#424651]/[0.15] bg-[#FFF2F1] py-2 max-sm:left-0 max-sm:mt-[0.6rem] max-sm:h-[90vw] max-sm:w-2/3 sm:right-0 sm:mt-4 sm:h-fit sm:w-[22.222222%] sm:rounded-bl-xl sm:shadow-lg">
				<h2
					class="w-fit border-b-2 border-[#424651]/25 pl-2 pr-6 text-5xl font-extrabold tracking-wider antialiased">
					Menu
				</h2>
				<ul class="w-fit pl-4">
					<li>
						<a
							href="https://github.com/TechFishe/Todo-App"
							target="_blank"
							rel="noopener noreferrer"
							on:click={() => (menuOpen = false)}>
							<svg
								xmlns="http://www.w3.org/2000/svg"
								fill="none"
								viewBox="0 0 24 24"
								stroke-width="1.5"
								stroke="currentColor">
								<path
									stroke-linecap="round"
									stroke-linejoin="round"
									d="M17.25 6.75L22.5 12l-5.25 5.25m-10.5 0L1.5 12l5.25-5.25m7.5-3l-4.5 16.5" />
							</svg>
							<span>Code</span>
						</a>
					</li>
				</ul>
			</aside>
		{/if} -->
	</nav>
</header>

<main class="mt-4">
	<slot />
</main>

<style>
	/* aside svg {
		width: 2rem;
		height: 2rem;
	}
	aside li {
		padding-top: 0.25rem;
		padding-bottom: 0.25rem;
	}
	aside span {
		font-size: 1.125rem;
		line-height: 1.75rem;
		font-weight: 500;
	}
	aside svg {
		width: 2rem;
		height: 2rem;
	}
	aside a {
		padding: 0.5rem 1.5rem 0.5rem 0.5rem;
		display: flex;
		align-items: center;
		justify-content: left;
		border-width: 1px;
		border-color: #fff2f1;
		border-radius: 0.375rem;
		@apply space-x-2 transition-all delay-75 duration-200 ease-in;
	}
	aside a:hover {
		color: #759fbc;
		border-color: rgb(66 70 81 / 0.5);
		@apply shadow-md shadow-[#759FBC]/75;
	} */

	nav div {
		width: 100%;
		height: fit-content;
		display: flex;
		align-items: center;
		justify-content: center;
	}
	nav div svg {
		width: 2.5rem;
		height: 2.5rem;
	}
	nav div a,
	button {
		padding: 0.375rem;
		border-width: 1px;
		border-color: #fff2f1;
		border-radius: 100%;
		@apply transition-all duration-200 ease-in;
	}
	nav div a:hover,
	button:hover {
		color: #759fbc;
		border-color: rgb(66 70 81 / 0.5);
		@apply shadow-md shadow-[#759FBC]/75;
	}
</style>
