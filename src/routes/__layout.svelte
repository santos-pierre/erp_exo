<script lang="ts">
	import Desktop from '../components/Sidebar/desktop.svelte';
	import Mobile from '../components/Sidebar/mobile.svelte';
	import type { NavLink } from 'src/types/NavLink';
	import '../app.css';

	let links: NavLink[] = [
		{
			name: 'Customers',
			slug: 'nav-customers',
			url: '/customers',
			iconPath: `<path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M12 4.354a4 4 0 110 5.292M15 21H3v-1a6 6 0 0112 0v1zm0 0h6v-1a6 6 0 00-9-5.197M13 7a4 4 0 11-8 0 4 4 0 018 0z"/>`
		},
		{
			name: 'Commands',
			slug: 'nav-commands',
			url: '/commands',
			iconPath: ` <path d="M9 17a2 2 0 11-4 0 2 2 0 014 0zM19 17a2 2 0 11-4 0 2 2 0 014 0z" /><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M13 16V6a1 1 0 00-1-1H4a1 1 0 00-1 1v10a1 1 0 001 1h1m8-1a1 1 0 01-1 1H9m4-1V8a1 1 0 011-1h2.586a1 1 0 01.707.293l3.414 3.414a1 1 0 01.293.707V16a1 1 0 01-1 1h-1m-6-1a1 1 0 001 1h1M5 17a2 2 0 104 0m-4 0a2 2 0 114 0m6 0a2 2 0 104 0m-4 0a2 2 0 114 0" />`
		},
		{
			name: 'Products',
			slug: 'nav-products',
			url: '/products',
			iconPath: `<path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M8 4H6a2 2 0 00-2 2v12a2 2 0 002 2h12a2 2 0 002-2V6a2 2 0 00-2-2h-2m-4-1v8m0 0l3-3m-3 3L9 8m-5 5h2.586a1 1 0 01.707.293l2.414 2.414a1 1 0 00.707.293h3.172a1 1 0 00.707-.293l2.414-2.414a1 1 0 01.707-.293H20" />`
		}
	];

	let openSidebar = false;
</script>

<div>
	<Mobile {links} open={openSidebar} on:close={() => (openSidebar = false)} />
	<Desktop {links} />
	<div class="flex flex-1 flex-col md:pl-64">
		<div class="sticky top-0 z-10 bg-gray-100 pl-1 pt-1 sm:pl-3 sm:pt-3 md:hidden">
			<button
				on:click={() => (openSidebar = true)}
				type="button"
				class="-ml-0.5 -mt-0.5 inline-flex h-12 w-12 items-center justify-center rounded-md text-gray-500 hover:text-gray-900 focus:outline-none focus:ring-2 focus:ring-inset focus:ring-indigo-500"
			>
				<span class="sr-only">Open sidebar</span>
				<!-- Heroicon name: outline/menu -->
				<svg
					class="h-6 w-6"
					xmlns="http://www.w3.org/2000/svg"
					fill="none"
					viewBox="0 0 24 24"
					stroke="currentColor"
					aria-hidden="true"
				>
					<path
						stroke-linecap="round"
						stroke-linejoin="round"
						stroke-width="2"
						d="M4 6h16M4 12h16M4 18h16"
					/>
				</svg>
			</button>
		</div>
		<main class="flex-1">
			<div class="py-6">
				<div class="mx-auto max-w-7xl px-4 sm:px-6 lg:px-8">
					<h1 class="text-2xl font-semibold text-gray-900">Dashboard</h1>
				</div>
				<div class="mx-auto max-w-7xl px-4 sm:px-6 md:px-8">
					<slot />
				</div>
			</div>
		</main>
	</div>
</div>
