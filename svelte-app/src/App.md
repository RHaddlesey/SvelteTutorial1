<script>
  import Modal from './Modal.svelte';

  let showModal = false;

  const toggleModal = () => {
    showModal = !showModal;
  }

  let people = [
    { name: "Richie", beltColour: "black", age: 50, id: 1 },
    { name: "Jeff", beltColour: "orange", age: 35, id: 2 },
    { name: "Veronica", beltColour: "brown", age: 45, id: 3 },
  ];

  const handleClick = (id) => {
    // delete person from people
    // console.log(id)
    people = people.filter((person) => person.id != id)
    // this checks if the person is the person = true/false. If it is true, it only returns that person... so we have to say if it is not true !=. That way, the people that do not = people will be returned instead. It is a bit backward, but makes sense because it is a truthy statement.
  }

  let num = 5;
</script>
<!-- 
{#if num > 20}
<p>Greater than 20!</p>
{:else if num > 5}
<p>Greater than 5!</p>
{:else}
<p>Not greater than 5!</p>
{/if} -->

<Modal {showModal} on:click={toggleModal}>
  <h3>Add a new person</h3>
  <form>
    <input type="text" placeholder="name">
    <input type="text" placeholder="belt colour">
    <button>Add person</button>
  </form>
  <!-- <div slot="title">
    <h3>Add a new person</h3>
  </div> this would create a named slot that only renders if the named slot is referenced in the parent. The stuff above that is not in a named tag will always render, but a name slot will only render if called. -->
</Modal>
<!-- here we are using svelte slots to pass this data back to the child -->
<main>
  <button on:click={toggleModal}>Open modal</button>
  {#each people as person (person.id)} 
  <!-- this adds a key into the array -->
  <div>
    <h4>{person.name}</h4>
    {#if person.beltColour === "black"}
    <p>
      <strong>Master NINJA!</strong>
    </p>
    {/if}
    <p>{person.age} years old, {person.beltColour} belt.</p>
    <button on:click={() => handleClick(person.id)}>delete</button>
  </div>
  {:else}
  <p>There are no data to show...</p>
  {/each}
</main>
<!-- the else is if there are no data, then output this. So if the array is empty, we still get an output to let us know it is empty! 
  // we have to make the event handler pass the data to the function. As in - (person.id) - but if we do that as just {handleClick(person.id)} then becuase we have a () it will invoke the function everytime, so we have to make it an arrow function so it is not invoked until the onClick event. So we wrap the function inside a function! -->

<style>
  main {
    text-align: center;
    padding: 1em;
    max-width: 240px;
    margin: 0 auto;
  }

  @media (min-width: 640px) {
    main {
      max-width: none;
    }
  }
</style>

