<script>
  import { createEventDispatcher } from "svelte";

  const dispatch = createEventDispatcher();

  export let todo;
</script>

<!-- svelte-ignore a11y-click-events-have-key-events -->
<li
  class="list-todo"
  class:border-slate-700={!todo.done}
  class:border-red-500={todo.done}
  class:text-red-500={todo.done}
  on:click={() => dispatch("click")}
>
  {todo.title}
</li>

<style>
  .list-todo {
    @apply col-span-4 p-4 py-8 text-center border-2 rounded cursor-pointer relative;
  }
  .todo-remove-btn {
    @apply absolute float-right;
  }
</style>
