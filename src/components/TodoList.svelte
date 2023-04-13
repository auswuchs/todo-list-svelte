<script>
  // @ts-nocheck
  let todos = [{ id: 0, title: "Hello, World!", done: true }];

  const toggleTodo = (id) => {
    const todo = todos.find((unit) => unit.id === id);
    todo.done = !todo.done;

    todos = todos;
  };

  const addTodo = (event) => {
    const data = new FormData(event.target);
    event.target.reset();

    todos = [
      ...todos,
      {
        id: todos.length,
        title: data.get("todo"),
        done: false,
      },
    ];
  };
</script>

<slot {todos} {toggleTodo} {addTodo} />
