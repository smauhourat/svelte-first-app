<script>
  import ContactCard from "./ContactCard.svelte";

  let name = "";
  let title = "";
  let image = "";
  let description = "";
  let formState = "empty";

  let createdContacts = [];

  function addContact() {
    if (
      name.trim().length == 0 ||
      title.trim().length == 0 ||
      image.trim().length == 0 ||
      description.trim().length == 0
    ) {
      formState = "invalid";
      return;
    }
    formState = "done";

    createdContacts = [
      ...createdContacts,
      {
        id: Math.random(),
        name: name,
        jobTitle: title,
        imageUrl: image,
        description: description,
      },
    ];
  }

  function delFirstContact() {
    createdContacts = createdContacts.slice(1);
  }

  const delContact = (id) => {
    //console.log(`delete ${id}`);
    createdContacts = createdContacts.filter((c) => c.id != id);
  };
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
  <button on:click={delFirstContact}>Delete First</button>
</div>

{#if formState == "invalid"}
  <p>Invalid inputs</p>
{:else if formState != "empty"}
  <p>Please enter some data and hit the button!</p>
{/if}

{#each createdContacts as contact}
  <h2># {contact.id}</h2>
  <ContactCard
    userName={contact.name}
    jobTitle={contact.jobTitle}
    userImage={contact.imageUrl}
    description={contact.description}
  />
  <button on:click={delContact(contact.id)}>Delete</button>
{:else}
  <p>Please start adding some contacts</p>
{/each}

<style>
  #form {
    width: 30rem;
    max-width: 100%;
  }
</style>
