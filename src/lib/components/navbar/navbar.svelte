<script lang="ts">
	import { page } from '$app/stores';

	// Input props
	export let github: string | null = null;
	export let logout_function: () => void = () => {};
	export let login_function: () => void = () => {};

	import Dropdown from '$lib/components/navbar/dropdown.svelte';

	interface Redirects {
		text: string;
		location: string;
	}
	const NavItems: Redirects[] = [
		{ text: 'Problems', location: '/problems' },
		{ text: 'Home', location: '/' }
	];
</script>

<title>ACM Algo</title>
<!-- Color gradient outline thing -->
<div class="gradient-border"></div>
<!-- Container for everything -->
<div class="navbar-container">
	<!-- Defines actual width: changes with screen width for mobile compatability -->
	<div class="nav-width">
		<!-- Left elements -->
		<div class="left-nav">
			<a href="https://acmcsuf.com" target="_blank" class="acm-badge">
				<img src="/icons/general-logo.svg" alt="ACM Logo" />
				<h3>at <b>CSUF</b></h3>
			</a>
		</div>
		<!-- Right elements -->
		<div class="right-nav">
			{#each NavItems as { text, location }}
				<div class="redirect-holder">
					<h3 class="redirect-text" class:active={$page.url.pathname === location.toLowerCase()}>
						<a href={location}>{text}</a>
					</h3>
				</div>
			{/each}
			{#if github}
				<div
					class="github-pfp"
					title="Logout"
					on:click={logout_function}
					on:keydown={(e) => {
						if (e.key === 'Enter') logout_function();
					}}
					tabindex="0"
					aria-pressed="false"
					role="button"
				>
					<img src={github} alt="Logout" />
				</div>
			{:else}
				<div class="redirect-holder">
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
						<h3 class="redirect-text">Login</h3>
					</div>
				</div>
			{/if}
		</div>
		<div class="dropdown-holder">
			<Dropdown {NavItems} />
		</div>
	</div>
</div>

<style>
	/* Styling for elements on the right */
	.right-nav {
		display: flex;
		justify-content: flex-end;
		align-items: center;
		height: 100%;
		width: 50%;
	}
	.redirect-holder {
		--padding: clamp(0.5rem, 1.5vw, 1.5rem);
		padding-left: var(--padding);
		padding-right: var(--padding);
	}
	.redirect-text {
		font-size: clamp(1.25rem, 1.75vw, 1.8rem);
		color: var(--text-color);
		transition: 0.2s;
	}
	.redirect-text.active {
		color: color-mix(in srgb, var(--algo-purple) 80%, white 20%);
		color: var(--algo-purple);
		text-decoration: underline;
	}
	.redirect-text:hover {
		color: color-mix(in srgb, var(--algo-purple) 80%, white 20%);
		transform: scale(1.05);
		cursor: pointer;
	}
	/* Styling the github pfp (logout) */
	.github-pfp {
		height: 60%;
		aspect-ratio: 1 / 1;
		margin-left: 3%;
		margin-right: 3%;
		border-radius: 50%;
		border: color-mix(in srgb, var(--algo-purple) 80%, transparent) solid 2px;
		transition: 0.2s;
	}
	.github-pfp img {
		height: 100%;
		width: 100%;
		object-fit: cover;
		border-radius: 50%;
	}
	.github-pfp:hover {
		transform: scale(1.05);
		-webkit-filter: drop-shadow(0px 0px 5px var(--algo-purple));
		filter: drop-shadow(0px 0px 5px var(--algo-purple));
		cursor: pointer;
	}
	/* Actually contains the navbar elements */
	.nav-width {
		z-index: 15;
		width: clamp(70%, 90%, 100%);
		height: 100%;
		display: flex;
		flex-flow: row nowrap;
		justify-content: space-between;
	}
	/* Styline for elements on the left (Just the acm badge pretty much) */
	.left-nav {
		display: flex;
		justify-content: flex-start;
		align-items: center;
		height: 100%;
		width: 50%;
	}
	.acm-badge {
		display: flex;
		align-items: center;
		height: 70%;
	}
	.acm-badge img {
		height: 100%;
		aspect-ratio: 1 / 1;
		object-fit: cover;
	}
	.acm-badge h3 {
		padding-left: 0.25rem;
		padding-right: 0.25rem;
		font-size: clamp(1rem, 1.75vw, 2rem);
	}
	/* Defines a container to store & size the navbar & add a gradient border color */
	.navbar-container {
		background-color: var(--bg-color);
		position: fixed;
		height: clamp(6rem, 12.5%, 100vh);
		z-index: 15;
		width: 100%;
		left: 0;
		top: 0;
		display: flex;
		justify-content: center;
		transition: 0.2s;
	}
	.gradient-border {
		z-index: 14;
		position: fixed;
		top: 0;
		left: 0;
		width: 100%;
		height: clamp(6.25rem, 13%, 100vh);
		background: linear-gradient(
			90deg,
			rgba(109, 98, 214, 1) 0%,
			rgba(95, 82, 209, 1) 50%,
			rgba(65, 50, 221, 1) 100%
		);
	}
	/* Changes navbar style on smaller screens */
	.dropdown-holder {
		display: flex;
		justify-content: flex-end;
		align-items: center;
		height: 100%;
		width: 50%;
		visibility: hidden;
		opacity: 0;
		pointer-events: none;
		position: absolute;
	}
	@media only screen and (max-width: 700px) {
		.nav-width {
			width: 95%;
		}
		.right-nav {
			visibility: hidden;
			opacity: 0;
			pointer-events: none;
			position: absolute;
		}
		.dropdown-holder {
			visibility: visible;
			opacity: 1;
			pointer-events: all;
			position: relative;
		}
	}
</style>
