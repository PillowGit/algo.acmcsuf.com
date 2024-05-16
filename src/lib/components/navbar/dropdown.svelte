<script lang="ts">
	interface Redirects {
		text: string;
		location: string;
	}
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
		{#each NavItems as { text, location }}
			<h3>{text}</h3>
		{/each}
	</div>
</div>

<style>
	/* Style button for dropdown */
	.button-holder {
		height: 37.5%;
		width: 100%;
		aspect-ratio: 1 / 1;
		margin-right: 5%;
		border: 1px solid red;
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
	/* Dropdown menu */
	.dropdown {
		position: fixed;
		top: 0;
		left: 0;
		background-color: color-mix(in srgb, var(--bg-color) 95%, white 5%);
		border-bottom: var(--complement2) 0.3vh solid;
		width: 100vw;
		height: 0;
		transition: 0.4s;
		z-index: -1;
		visibility: hidden;
		opacity: 0;
		pointer-events: none;
		display: flex;
		flex-direction: column;
	}
	.dropdown.active {
		min-height: 13vh;
		z-index: 21;
		visibility: visible;
		opacity: 1;
		pointer-events: all;
	}
</style>
