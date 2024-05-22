<script lang="ts">
	import { page } from '$app/stores';
	interface Redirects {
		text: string;
		location: string;
	}

	// Input props
	export let github: string | null = null;
	export let username: string | null = null;
	export let logout_function: () => void = () => {};
	export let login_function: () => void = () => {};
	export let NavItems: Redirects[] = [];

	let dropdown_open: boolean = false;
</script>

<div class="button-holder">
	<div
		class="button-click"
		title="Logout"
		on:click={() => {
			dropdown_open = true;
		}}
		on:keydown={(e) => {
			if (e.key === 'Enter') dropdown_open = true;
		}}
		tabindex="0"
		aria-pressed="false"
		role="button"
	>
		<img src="/icons/menu.svg" alt="Menu" class="dropdown-button" />
	</div>
	<div
		class="dropdown-bg"
		class:active={dropdown_open}
		title="Unfocus"
		on:click={() => {
			dropdown_open = false;
		}}
		on:keydown={(e) => {
			if (e.key === 'Enter') dropdown_open = false;
		}}
		tabindex="0"
		aria-pressed="false"
		role="button"
	></div>
	<div class="dropdown" class:active={dropdown_open}>
		<div class="dropdown-item-space"></div>
		{#each NavItems.entries() as [_, item]}
			<h3 class="section-choice" class:active={$page.url.pathname === item.location.toLowerCase()}>
				<a href={item.location}>{item.text}</a>
			</h3>
			<div class="divider"></div>
		{/each}
		{#if github}
			<div
				title="Logout"
				on:click={logout_function}
				on:keydown={(e) => {
					if (e.key === 'Enter') logout_function();
				}}
				tabindex="0"
				aria-pressed="false"
				role="button"
			>
				<h3 class="section-choice">
					Signed in as <span style="color: var(--algo-purple);">{username}</span>. Click to logout.
				</h3>
			</div>
		{:else}
			<div
				title="Login with GitHub"
				on:click={login_function}
				on:keydown={(e) => {
					if (e.key === 'Enter') login_function();
				}}
				tabindex="0"
				aria-pressed="false"
				role="button"
			>
				<h3 class="section-choice">Login</h3>
			</div>
		{/if}
		<div class="dropdown-item-space"></div>
	</div>
</div>

<style>
	/* Style Dropdown Elements */
	.section-choice {
		font-size: clamp(1rem, 1.45rem, 1.75rem);
		text-align: center;
		text-wrap: evenly;
		transition: 0.2s;
	}
	.section-choice.active {
		color: color-mix(in srgb, var(--algo-purple) 80%, white 20%);
		color: var(--algo-purple);
		text-decoration: underline;
	}
	.section-choice:hover {
		color: color-mix(in srgb, var(--algo-purple) 80%, white 20%);
		transform: scale(1.05);
		cursor: pointer;
	}

	.divider {
		margin-top: 1vh;
		margin-bottom: 1vh;
		height: 0.2vh;
		width: 60%;
		background-color: color-mix(in srgb, var(--complement2) 60%, transparent 40%);
		border-radius: 50%;
	}

	.dropdown-item-space {
		padding-top: 2vh;
		padding-bottom: 2vh;
		width: 5vw;
	}
	/* Dropdown menu */
	.dropdown {
		position: fixed;
		top: 0;
		left: 0;
		background-color: color-mix(in srgb, var(--bg-color) 95%, white 5%);
		border-bottom: var(--complement2) 0.3vh solid;
		width: 100vw;
		min-height: 13vh;
		transition: 0.4s;
		z-index: -1;
		visibility: hidden;
		opacity: 0;
		pointer-events: none;
		display: flex;
		flex-direction: column-reverse;
		align-items: center;
		justify-content: center;
	}
	.dropdown.active {
		z-index: 21;
		visibility: visible;
		opacity: 1;
		pointer-events: all;
	}
	/* Screen unfocus effect */
	.dropdown-bg {
		position: fixed;
		top: 0;
		left: 0;
		height: 100%;
		width: 100%;
		background-color: color-mix(in srgb, var(--bg-color) 100%, transparent 50%);
		transition: 0.4s;
		z-index: -1;
		visibility: hidden;
		opacity: 0;
		pointer-events: none;
	}
	.dropdown-bg.active {
		z-index: 19;
		visibility: visible;
		opacity: 1;
		pointer-events: all;
	}
	/* Style button for dropdown */
	.button-holder {
		height: 37.5%;
		width: 100%;
		aspect-ratio: 1 / 1;
		margin-right: 5%;
		flex-direction: row;
	}
	.button-click {
		height: 100%;
		margin-left: auto;
		aspect-ratio: 1 / 1;
		z-index: 20;
	}
	.dropdown-button {
		height: 100%;
		aspect-ratio: 1 / 1;
		object-fit: cover;
		-webkit-filter: invert(1);
		filter: invert(1);
	}
</style>
