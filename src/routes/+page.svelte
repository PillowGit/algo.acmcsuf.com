<script lang="ts">
	// Get Page Data from load
	export let data;
	// Extract supabase from data
	let { supabase } = data;
	$: ({ supabase } = data);

	async function login() {
		await supabase.auth.signInWithOAuth({
			provider: 'github',
			options: {
				redirectTo: 'http://localhost:5173/'
			}
		});
	}
	async function logout() {
		await supabase.auth.signOut();
		window.location = '/';
	}
</script>

<button on:click={login}>login</button>
<button on:click={logout}>logout</button>
