<script lang="ts">
	import { onMount } from 'svelte';

	// Import components
	import Navbar from '$lib/components/navbar.svelte';
	import Footer from '$lib/components/footer.svelte';
	import '../tail.css';

	// Import and check supabase for github info
	export let data;
	let { supabase } = data;
	$: ({ supabase } = data);

	let github_display = '';

	onMount(async () => {
		const userdata = await supabase.auth.getUser();
		if (!userdata) return;
		github_display = userdata.data.user.user_metadata.avatar_url;
	});
</script>

<Navbar github={github_display} />
<div class="page">
	<div class="page-content">
		<slot />
	</div>
	<Footer />
</div>

<style>
	.page {
		position: absolute;
		top: 0;
		left: 0;

		min-height: 100vh;
		width: 100%;

		display: flex;
		flex-flow: column;
		align-items: center;
		justify-content: space-between;
	}

	.page-content {
		padding-top: 20vh;
		width: 70%;

		display: flex;
		flex-flow: column;
		align-items: center;
	}
	@media only screen and (max-width: 768px) {
		.page-content {
			width: 100%;
			margin-left: 0;
			margin-right: 0;
		}
	}
</style>
