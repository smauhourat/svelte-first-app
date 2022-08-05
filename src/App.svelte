<script>
  import ContactCard from "./ContactCard.svelte";

  let name = "Max";
  let title = "";
  let image = "";
  let description = "";
  let formState = "empty";

  let createdContact;

  function addContact() {
    if (
      name.trim().length == 0 ||
      title.trim().length == 0 ||
      image.trim().length == 0 ||
      description.trim().length == 0
    ) {
      formState = "invalid";
    }
    formState = "done";
    //console.log(image);
    createdContact = {
      name: name,
      jobTitle: title,
      imageUrl: image,
      description: description,
    };
    console.log(JSON.stringify(createdContact));
  }
</script>

<div id="form">
  <div class="form-control">
    <label for="userName">User Name</label>
    <input type="text" bind:value={name} id="userName" />
  </div>
  <div class="form-control">
    <label for="jobTitle">Job Title</label>
    <input type="text" bind:value={title} id="jobTitle" />
  </div>
  <div class="form-control">
    <label for="image">Image URL</label>
    <input type="text" bind:value={image} id="image" />
  </div>
  <div class="form-control">
    <label for="desc">Description</label>
    <textarea rows="3" bind:value={description} id="desc" />
  </div>
  <button on:click={addContact}>Add Contact</button>
</div>
{#if formState === "done"}
  <ContactCard
    userName={createdContact.name}
    jobTitle={createdContact.jobTitle}
    userImage={createdContact.imageUrl}
    description={createdContact.description}
  />
{:else if formState == "invalid"}
  <p>Invalid inputs</p>
{:else}
  <p>Please enter some data and hit the button!</p>
{/if}

<style>
  #form {
    width: 30rem;
    max-width: 100%;
  }
</style>
