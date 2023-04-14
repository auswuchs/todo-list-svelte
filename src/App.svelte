<script>
  // @ts-nocheck
  import TodoList from "./components/TodoList.svelte";

  const heading = "TodoList.svelte";
</script>

<main>
  <h1 class="heading">{heading}</h1>

  <TodoList let:todos let:toggleTodo let:addTodo>
    <ul class="list">
      {#each todos as todo (todo.id)}
        <!-- svelte-ignore a11y-click-events-have-key-events -->
        <li
          class="list-todo"
          class:border-slate-700={!todo.done}
          class:border-red-500={todo.done}
          class:text-red-500={todo.done}
          on:click={toggleTodo(todo.id)}
        >
          {todo.title}
        </li>
      {/each}

      <form on:submit|preventDefault={addTodo} class="todo-form">
        <input
          type="text"
          name="todo"
          class="todo-form-input"
          autocomplete="off"
          placeholder="New Todo"
        />
      </form>
    </ul>
  </TodoList>
</main>

<style>
  .heading {
    @apply font-bold;
  }

  .list {
    @apply grid grid-cols-12 gap-6 mt-12;
  }

  .list-todo {
    @apply col-span-4 p-4 py-8 text-center border-2 rounded cursor-pointer;
  }

  .todo-form {
    @apply col-span-4 p-4 py-8 border-2 border-slate-700 border-dashed rounded;
  }

  .todo-form-input {
    @apply bg-transparent border-b-2 border-slate-700 outline-none w-full;
  }
</style>
