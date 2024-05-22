<script lang="ts">
	// All icons used in this site are from here:
	// https://svgrepo.com/collection/iconhub-glyph-icons/

	import { page } from '$app/stores';
	import { onMount } from 'svelte';

	// Import components
	import Navbar from '$lib/components/navbar/navbar.svelte';
	import Footer from '$lib/components/footer.svelte';
	import '../tail.css';

	// Import and check supabase for github info
	export let data;
	let { supabase } = data;
	$: ({ supabase } = data);

	let github_display = '';
	let github_username = '';

	onMount(async () => {
		const userdata: any = await supabase.auth.getUser();
		if (!userdata) return;
		else {
			github_username = userdata.data.user.user_metadata.user_name;
			github_display = userdata.data.user.user_metadata.avatar_url;
		}
	});
	async function logout() {
		if (window.confirm('Logout?')) {
			await supabase.auth.signOut();
			location.reload();
		}
	}
	async function login() {
		await supabase.auth.signInWithOAuth({
			provider: 'github',
			options: {
				redirectTo: $page.url.toString()
			}
		});
	}
</script>

<Navbar
	github={github_display}
	username={github_username}
	logout_function={logout}
	login_function={login}
/>
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
