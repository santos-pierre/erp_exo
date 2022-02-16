<script lang="typescript">
	import type { NavLink } from 'src/types/NavLink';
	import { linear } from 'svelte/easing';
	import { fade } from 'svelte/transition';
	import { page } from '$app/stores';

	let open = false;

	export const router = false;

	export let links: NavLink[];

	const translate = (_node, { duration = 300 }) => {
		return {
			duration,
			css: (t: any) => {
				const eased = linear(t);
				return `
                    transform: translateX(-${100 - eased * 100}%);
                `;
			}
		};
	};
</script>

<button on:click={() => (open = true)}>Open</button>

{#if open}
	<div class="fixed inset-0 z-40 flex md:hidden" role="dialog" aria-modal="true">
		<div
			class="fixed inset-0 bg-gray-600 bg-opacity-75"
			aria-hidden="true"
			transition:fade={{ duration: 300, easing: linear }}
			on:click={() => (open = false)}
		/>
		<div class="relative flex w-full max-w-xs flex-1 flex-col bg-gray-800" transition:translate>
			<div
				class="absolute top-0 right-0 -mr-12 pt-2"
				transition:fade={{ duration: 300, easing: linear }}
			>
				<button
					type="button"
					class="ml-1 flex h-10 w-10 items-center justify-center rounded-full focus:outline-none focus:ring-2 focus:ring-inset focus:ring-white"
					on:click={() => (open = false)}
				>
					<span class="sr-only">Close sidebar</span>
					<!-- Heroicon name: outline/x -->
					<svg
						class="h-6 w-6 text-white"
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
							d="M6 18L18 6M6 6l12 12"
						/>
					</svg>
				</button>
			</div>

			<div class="h-0 flex-1 overflow-y-auto pt-5 pb-4">
				<h2 class="ml-2 text-2xl font-bold leading-7 text-gray-900 sm:truncate sm:text-3xl">
					ERP-BF
				</h2>
				<nav class="mt-5 space-y-1 px-2">
					{#each links as link (link.slug)}
						<a
							href={link.url}
							class="{$page.url.pathname.includes(link.url)
								? 'bg-gray-900 text-white'
								: 'text-gray-300 hover:bg-gray-700 hover:text-white'}
							group flex items-center rounded-md px-2 py-2 text-base font-medium text-gray-300 hover:bg-gray-700 hover:text-white"
						>
							<svg
								class="{$page.url.pathname === 'customers'
									? 'text-gray-300'
									: 'text-gray-400 group-hover:text-gray-300'}
								mr-4 h-6 w-6 flex-shrink-0 text-gray-400 group-hover:text-gray-300"
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

		<div class="w-14 flex-shrink-0">
			<!-- Force sidebar to shrink to fit close icon -->
		</div>
	</div>
{/if}
