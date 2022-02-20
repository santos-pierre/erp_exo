<script lang="ts">
	import type { NavLink } from 'src/types/NavLink';
	import { page } from '$app/stores';
	export let links: NavLink[];
</script>

<div class="hidden md:fixed md:inset-y-0 md:flex md:w-64 md:flex-col">
	<div class="flex min-h-0 flex-1 flex-col bg-gray-800">
		<div class="flex flex-1 flex-col overflow-y-auto pt-5 pb-4">
			<div class="flex flex-shrink-0 items-center px-4">
				<h2 class="ml-2 text-2xl font-bold leading-7 text-gray-900 sm:truncate sm:text-3xl">
					ERP-BF
				</h2>
			</div>
			<nav class="mt-5 flex-1 space-y-1 px-2">
				{#each links as link (link.slug)}
					<a
						href={link.url}
						class="{$page.url.pathname.includes(link.url)
							? 'bg-gray-900 text-white'
							: 'text-gray-300 hover:bg-gray-700 hover:text-white'} group flex items-center rounded-md px-2 py-2 text-sm font-medium"
					>
						<svg
							class="{$page.url.pathname.includes(link.url)
								? 'text-gray-300'
								: 'text-gray-400 group-hover:text-gray-300'} mr-3 h-6 w-6 flex-shrink-0 "
							xmlns="http://www.w3.org/2000/svg"
							fill="none"
							viewBox="0 0 24 24"
							stroke="currentColor"
							aria-hidden="true"
						>
							{@html link.iconPath}
						</svg>
						{link.name}
					</a>
				{/each}
			</nav>
		</div>
	</div>
</div>
