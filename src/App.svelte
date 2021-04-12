<script>
  import createSvelidation from 'svelidation';

  const { createForm, createEntry } = createSvelidation();

  const [ nameErrors, nameValue, nameInput ] = createEntry({
    type: 'string',
    required: true,
    value: ''
  });

  const [ emailErrors, emailValue, emailInput ] = createEntry({
    type: 'email',
    required: true,
    value: ''
  });

  const [ passwordErrors, passwordValue, passwordInput ] = createEntry({
    type: 'string',
    min: 3,
    required: true,
    value: ''
  });

  const onSuccess = (values) => {
    console.log(values);
  };

  $: console.log('Erros do input nome:', $nameErrors);
  $: console.log('Erros do input e-mail:', $emailErrors);
  $: console.log('Erros do input senha:', $passwordErrors);
</script>

<form use:createForm={{ onSuccess }} on:submit|preventDefault>
  <div>
    <label>Nome</label>
    <input type="text" bind:value={$nameValue} use:nameInput placeholder="Digite o nome aqui..." />
    
    {#if $nameErrors.includes('required')}
      <p>Nome é obrigatório</p>
    {/if}
  </div>

  <div>
    <label>E-mail</label>
    <input type="email" bind:value={$emailValue} use:emailInput placeholder="Digite o e-mail aqui..." />
    
    {#if $emailErrors.includes('required')}
      <p>E-mail é obrigatório</p>
    {/if}

    {#if $emailErrors.includes('type')}
      <p>Deve ser um formato de e-mail válido</p>
    {/if}
  </div>

  <div>
    <label>Senha</label>
    <input type="password" bind:value={$passwordValue} use:passwordInput placeholder="Digite a senha aqui..." />

    {#if $passwordErrors.includes('required')}
      <p>Senha é obrigatória</p>
    {/if}

    {#if $passwordErrors.includes('min')}
      <p>Deve conter ao menos 3 dígitos</p>
    {/if}
  </div>

  <button type="submit">Enviar</button>
</form>

<style lang="scss">
	* {
    margin: 0;
    padding: 0;
    box-sizing: border-box;
  }

  label {
    margin-bottom: 10px;
    font-size: 1.1rem;
  }

  input {
    padding: 5px;
    outline: none;
  }

  form {
    width: 20%;
    display: block;
    padding: 20px;
    margin: 5px;
    background-color: whitesmoke;
    border-radius: 5%;
  }

  div {
    display: flex;
    flex-direction: column;

    &:not(:first-of-type) {
      margin-top: 30px;
    }
  }

  button {
    margin-top: 30px;
    padding: 10px 20px;
    width: 100%;
    outline: none;

    transition: filter 0.2s;

    &:hover {
      filter: brightness(0.9);
    }
  }

  p {
    font-size: 1.1rem;
    margin-top: 7px;
    color: rgb(179, 13, 13);
  }

</style>