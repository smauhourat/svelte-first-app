<script>
  import ContacCard from './ContacCard.svelte';

  let name = 'San';
  let age = 30;

  $: uppercaseName = name.toUpperCase();

  $: console.log(name);

  $: if (name === 'Santiago') {
    console.log('Its run!');
    age = 20;
  }

  function changeName() {
    name = 'Santiago';
  }

  function incrementAge() {
    age += 1;
  }

  function handleInput(event) {
    name = event.target.value;
  }
</script>

<h1>Hello {uppercaseName}, my age is {age}!</h1>
<input type="text" value={name} on:input={handleInput} />
<input type="text" bind:value={name} />
<button on:click={incrementAge}>Change Age</button>
<button on:click={changeName}>Change Name</button>

<ContacCard />

<style>
  h1 {
    color: purple;
  }
</style>
