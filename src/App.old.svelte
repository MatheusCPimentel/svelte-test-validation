<script>
	let name;
	let email;
	let password; 

	function handleSubmit(e) {
		e.preventDefault();

		console.log('Nome:', name);
		console.log('E-mail:', email);
		console.log('Password:', password);
	}

</script>

<main>
	<form>
		<div>
			<label>Nome</label>
			<input bind:value={name} placeholder="Digite o nome aqui..." />
		</div>
		
		<div>
			<label>E-mail</label>
			<input bind:value={email} placeholder="Digite o e-mail aqui..." />
		</div>
		
		<div>
			<label>Senha</label>
			<input type="password" bind:value={password} placeholder="Digite a senha aqui..." />
		</div>

		<button type="submit" on:click={handleSubmit}>Submit</button>
	</form>
</main>

<style>
	form {
		margin: 10px;
	}

	label {
		margin-bottom: 5px;
	}

	input {
		margin-bottom: 20px;
	}

</style>