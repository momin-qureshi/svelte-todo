<script>
  let todoItems = [];
  let newItem = "";

  function addTodoItem() {
    newItem = newItem.trim();
    if (newItem.length == 0) {
      return;
    }

    const todo = {
      text: newItem,
      checked: false,
      id: Date.now(),
    };

    todoItems = [
      ...todoItems,
      {
        text: newItem,
        checked: false,
        id: Date.now(),
      },
    ];
    newItem = "";
  }

  function toggleItemDone(id) {
    todoItems = todoItems.map((item) => {
      if (item.id === id) {
        item.checked = !item.checked;
      }
      return item;
    });
  }

  function deleteTodoItem(id) {
    todoItems = todoItems.filter((item) => item.id !== Number(id));
  }
</script>

<main>
  <div class="container">
    <h1 class="title">todos</h1>
    <ul class="todo-list">
      {#each todoItems as todo (todo.id)}
        <li class="todo-item {todo.checked? 'done': ''}">
          <input
            id={todo.id}
            type="checkbox"
            on:click={() => toggleItemDone(todo.id)}
          />
          <label for={todo.id} />
          <span class="todo-text">{todo.text}</span>
          <button
            class="delete-button"
            on:click={() => deleteTodoItem(todo.id)}
          >
            <svg class="icon"><use href="#delete-icon" /></svg>
          </button>
        </li>
      {/each}
    </ul>
    <form on:submit|preventDefault={addTodoItem}>
      <input
        class="todo-input"
        type="text"
        aria-label="Enter a new todo item"
        placeholder="E.g. Build a web app"
        bind:value={newItem}
      />
      <button class="add-button" type="submit">Add</button>
    </form>
  </div>
</main>
