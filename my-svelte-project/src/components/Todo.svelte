<script lang="ts">
  let items = [];
  let newItem = "";

  function addItem() {
    newItem = newItem.trim();
    if (!newItem) return;

    const todo = {
      text: newItem,
      id: Date.now(),
    };

    items = [...items, todo];
    newItem = "";
  }

  function deleteItem(id) {
    items = items.filter((item) => item.id !== Number(id));
  }
</script>

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

<main>
  <h2>To-Do List</h2>
  <form on:submit|preventDefault={addItem}>
    <input
      type="text"
      aria-label="Enter a new todo item"
      placeholder="E.g. Take a svelte course"
      bind:value={newItem} />
  </form>
  <ul>
    {#each items as todo (todo.id)}
      <li>
        <p>{todo.text}</p>
        <button on:click={() => deleteItem(todo.id)}>X</button>
      </li>
    {/each}
  </ul>

</main>
