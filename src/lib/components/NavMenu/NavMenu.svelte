<script lang="ts">
	import { page } from '$app/stores';
	import { HOME, NavBar } from '$lib/params';
	import { theme, toggleTheme } from '$lib/stores/theme';

	import { base } from '$app/paths';
	import UIcon from '../Icon/UIcon.svelte';

	let currentRoute = '/';

	$: {
		if ($page) {
			currentRoute = $page.url.pathname;

			// console.log(currentRoute);
		}
	}

	const items = [
		{ title: NavBar.sign_up, to: '/sign-up', icon: 'i-carbon-sigma'},
		{ title: NavBar.projects, to: '/projects', icon: 'i-carbon-color-palette' },
		{ title: NavBar.about, to: '/about', icon: 'i-carbon-logo-ansible-community' },
		{ title: NavBar.map, to: '/map', icon: 'i-carbon-globe' }
	];
</script>

<div class="nav-menu">
	<nav class="container !justify-between flex flex-row items-center text-sm">
		<a
			href={`${base}/`}
			class="nav-menu-left decoration-none flex flex-row items-center cursor-pointer px-4 text-[var(--secondary-text)] self-stretch hover:bg-[color:var(--main-hover)]"
		>
			<UIcon icon="i-carbon-aperture" classes="text-2em" />
			<span class="ml-2 text-md font-bold hidden md:inline">{HOME.name}</span>
		</a>
		<div class="flex flex-row flex-1 self-center justify-center">
			{#each items as item}
				<a href={`${base}${item.to}`} class="nav-menu-item !text-[var(--secondary-text)]">
					<UIcon icon={item.icon} classes="text-1.3em" />
					<span class="nav-menu-item-label">{item.title}</span>
				</a>
			{/each}
			<a
				href="https://www.instagram.com/sans.honte.press?igsh=MTRnZjRobW80Y3g0Zw%3D%3D&utm_source=qr"
				class="nav-menu-item !text-[var(--secondary-text)]"
				target="_blank"
			>
				<UIcon icon="i-carbon-aperture" classes="text-1.3em" />
				<span class="nav-menu-item-label">Instagram</span>
			</a>
		</div>
		<div class="flex flex-row self-stretch items-stretch gap-1 text-1.15em">
			<a
				href={`${base}/search`}
				class="text-inherit col-center self-stretch px-2 hover:bg-[color:var(--main-hover)]"
			>
				<UIcon icon="i-carbon-search" />
			</a>
			<button
				class="bg-transparent text-1em border-none cursor-pointer hover:bg-[color:var(--main-hover)] text-[var(--secondary-text)] px-2"
				on:click={() => toggleTheme()}
			>
				{#if $theme}
					<UIcon icon="i-carbon-moon" />
				{:else}
					<UIcon icon="i-carbon-sun" />
				{/if}
			</button>
		</div>
	</nav>
</div>

<style lang="scss">
	.nav-menu {
		display: flex;
		justify-content: center;
		position: sticky;
		top: 0px;
		z-index: 10;
		padding: 0px 10px;
		border-bottom: 1px solid var(--secondary);
		background-color: var(--main);

		&-item {
			text-decoration: none;
			font-weight: 400;
			padding: 10px 20px;
			color: inherit;
			display: flex;
			align-items: center;
			border-bottom: 3px solid transparent;

			&-label {
				margin-left: 10px;

				@media (max-width: 950px) {
					& {
						display: none;
					}
				}
			}

			&:hover {
				background-color: var(--main-hover);
			}
		}
	}
</style>
