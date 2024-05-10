<script lang="ts">
	// Input props
	export let github: string | null = null;
</script>

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
			{#if github}
				<img src={github} alt="Your Github Avatar" class="github-pfp" />
			{:else}{/if}
		</div>
	</div>
</div>

<style>
	/* Styline for elements on the left */
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
	/* Styling for elements on the right */
	.right-nav {
		display: flex;
		justify-content: flex-end;
		align-items: center;
		height: 100%;
		width: 50%;
	}
	/* Styling the github pfp specifically */
	.github-pfp {
		height: 60%;
		aspect-ratio: 1 / 1;
		margin-left: 3%;
		margin-right: 3%;
		border-radius: 50%;
		border: color-mix(in srgb, var(--algo-purple) 80%, transparent) solid 2px;
		transition: 0.2s;
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
		width: 70%;
		height: 100%;
		display: flex;
		flex-flow: row nowrap;
		justify-content: space-between;
	}
	/* Wraps a div with styling around the entire page */
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
	@media only screen and (max-width: 600px) {
		.nav-width {
			width: 95%;
		}
	}
</style>
