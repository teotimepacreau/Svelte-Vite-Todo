<script>
  import AddTodo from "./AddTodo.svelte";

  import Todo from "./Todo.svelte";
  // state
  let todos = [
    { id: "1e4a59703af84", text: "Todo 1", completed: true },
    { id: "9e09bcd7b9349", text: "Todo 2", completed: false },
    { id: "9e4273a51a37c", text: "Todo 3", completed: false },
    { id: "53ae48bf605cc", text: "Todo 4", completed: false },
  ];

  $: todosAmount = todos.length;

  function generateRandomId() {
    return Math.random().toString(16).slice(2);
  }

  // text est récupéré depuis l'évènement dispatché dans AddTodo.svelte
  const addTodoItem = (text) => {
    const item = {
      id: generateRandomId(),
      text: text.detail,
      completed: false,
    };
    todos.unshift(item);
    todos = todos;
  };

  // état "complété" et vice versa
  const completeTodo = (id) => {
    todos.forEach((todo)=>{
      if(todo.id === id){
        todo.completed = !todo.completed
      }
    })
    todos = todos
  }

  // supprimer tâche
  const removeTodo = (id)=> 
  todos = todos.filter((item)=>{
    return item.id !== id
  })
</script>

<main>
  <h1 class="title">todos</h1>

  <section class="todos">
    <AddTodo on:add-todo-item={addTodoItem} />
    <ul class="todo-list">
      {#each todos as todo (todo.id)}
        <Todo {todo} {completeTodo}{removeTodo} />
      {/each}
    </ul>

    <div class="actions">
      <span class="todo-count">0 left</span>
      <div class="filters">
        <button class="filter">All</button>
        <button class="filter">Active</button>
        <button class="filter">Completed</button>
      </div>
      <button class="clear-completed">Clear completed</button>
    </div>
  </section>
</main>

<style>
  /* Todos */

  .title {
    font-size: var(--font-80);
    font-weight: inherit;
    text-align: center;
    color: var(--color-title);
  }

  .todos {
    --width: 500px;
    --todos-bg: hsl(0 0% 98%);
    --todos-text: hsl(220 20% 14%);

    color: var(--todos-text);
    background-color: var(--todos-bg);
  }

  .todo-list {
    list-style: none;
  }

  .actions {
    position: relative;
    display: flex;
    align-items: center;
    justify-content: space-between;
    padding: var(--spacing-8) var(--spacing-16);
    font-size: 0.9rem;
    border-top: 1px solid var(--color-gray-90);
  }

  .actions:before {
    content: "";
    height: 40px;
    position: absolute;
    right: 0;
    bottom: 0;
    left: 0;
    box-shadow:
      0 1px 1px hsla(0, 0%, 0%, 0.2),
      0 8px 0 -3px hsl(0, 0%, 96%),
      0 9px 1px -3px hsla(0, 0%, 0%, 0.2),
      0 16px 0 -6px hsl(0, 0%, 96%),
      0 17px 2px -6px hsla(0, 0%, 0%, 0.2);
    z-index: -1;
  }



  /* Filters */

  .filters {
    display: flex;
    gap: var(--spacing-4);
  }

  .filter {
    text-transform: capitalize;
    padding: var(--spacing-4) var(--spacing-8);
    border: 1px solid transparent;
    border-radius: var(--radius-base);
  }

  .filter:hover {
    border: 1px solid var(--color-highlight);
  }

  .selected {
    border-color: var(--color-highlight);
  }
</style>
