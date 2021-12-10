<script>
	const formData = {}
	const submit = async () => {
		const res = await fetch('/api/sendMail', {
			method:'POST',
			headers: {
					'Content-Type': 'application/json;charset=utf-8'
				},
				body: JSON.stringify(formData)
		})
		const res1 = await res.json();
		console.log(res1);
	}
</script>

<main>
	<!-- forma with inputs -->
	<form on:submit|preventDefault={submit}>
		<input name="email" type="email" placeholder="Enter your email" bind:value={formData.emai}/>
		<input name="name" type="text" placeholder="Enter your name" bind:value={formData.name}/>
		<input name="password" type="password" placeholder="Enter your password" bind:value={formData.password}/>
		<input name="confirmPassword" type="password" placeholder="Confirm password" bind:value={formData.confirmPassword}/>
		<input type="submit"/>
	</form>
</main>

<style>
	main {
		text-align: center;
		padding: 1em;
		max-width: 240px;
		margin: 0 auto;
	}

</style>