<script>
  import ContacCard from './ContacCard.svelte';

  let name = '';
  let jobTitle = '';
  let image = '';
  let description = '';
  let userImage = '';
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
<!-- <input type="text" value={name} on:input={handleInput} /> -->
<input type="text" bind:value={name} placeholder="User Name..." />
<input type="text" bind:value={jobTitle} placeholder="Job Title..." />
<input type="text" bind:value={userImage} placeholder="User Image..." />
<textarea rows="3" bind:value={description} />

<button on:click={incrementAge}>Change Age</button>
<!-- <button on:click={changeName}>Change Name</button> -->

<ContacCard userName={uppercaseName} {jobTitle} {description} {userImage} />

<style>
  h1 {
    color: purple;
  }
</style>
