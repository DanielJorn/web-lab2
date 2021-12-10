<script>
	import {writable} from 'svelte/store'
	let isLoading = false;
	let result = writable("")
	const formData = {}
	const submit = async () => {
		isLoading=true;
		const res = await fetch('/api/sendMail', {
			method:'POST',
			headers: {
					'Content-Type': 'application/json;charset=utf-8'
				},
				body: JSON.stringify(formData)
		})
		const res1 = await res.json();
		result.set(res1.result.success?"email was sent":"error occured");
		isLoading=false
	}
</script>

<main>
	{#if isLoading}
	<div class="loader">
		<img src="../loader.gif" alt="loader" />
	  </div>
	{:else}  
	<form on:submit|preventDefault={submit}>
		<input name="email" type="email" placeholder="Enter your email" bind:value={formData.email}/>
		<input name="name" type="text" placeholder="Enter your name" bind:value={formData.name}/>
		<input name="password" type="password" placeholder="Enter your password" bind:value={formData.password}/>
		<input name="confirmPassword" type="password" placeholder="Confirm password" bind:value={formData.confirmPassword}/>
		<input type="submit" disabled={isLoading}/>
	</form>
	<div>
		<p>{$result}</p>
	</div>

	{/if}
</main>

<style>
	main {
		text-align: center;
		padding: 1em;
		max-width: 240px;
		margin: 0 auto;
	}

</style>