<script>
  //PSEUDO CODE : au clic sur le bouton submit, ce qui est entré dans l'input s'ajoute à la liste
  import {createEventDispatcher} from 'svelte'
  const dispatch = createEventDispatcher()

  let text
  const handleAddTodoItemToList = ()=>{
    dispatch('add-todo-item', text)
  }

</script>

<form>
  <input bind:value = {text}
    id="new-todo"
    class="new-todo"
    placeholder="What needs to be done?"
    type="text"
  />
  <button on:click|preventDefault={handleAddTodoItemToList} type="submit">Add</button>
</form>

<style>
  /* Add todo */
    form {
        display: flex;
        justify-content: space-between;
    }
    form button {
        background-color: #B63E44;
        overflow: hidden;
        padding-inline: 2ch;
        color: white;
    }
  .toggle-all {
    width: 1px;
    height: 1px;
    position: absolute;
    opacity: 0;
  }

  .toggle-all + label {
    position: absolute;
    font-size: 0;
  }

  .toggle-all + label:before {
    content: "❯";
    display: block;
    padding: var(--spacing-16);
    font-size: var(--font-24);
    color: var(--color-gray-58);
    transform: rotate(90deg);
  }

  .toggle-all:checked + label:before {
    color: var(--color-gray-28);
  }

  .new-todo {
    width: 100%;
    padding: var(--spacing-16);
    padding-left: 60px;
    font-size: var(--font-24);
    border: none;
    border-bottom: 1px solid var(--shadow-1);
  }
</style>
