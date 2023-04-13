<script>
  export let todos = [];

  let toggleTodo = (id) => {
    const todo = todos.find((unit) => (unit.id = id));
    todo.done = !todo.done;
  };

  let addTodo = (event) => {
    const data = new FormData(event.target);
    event.target.reset();

    console.warn({ todos });
    todos.push({
      id: todos.length,
      title: data.get("todo"),
      done: false,
    });
  };
</script>

<slot {todos} {toggleTodo} {addTodo} />
