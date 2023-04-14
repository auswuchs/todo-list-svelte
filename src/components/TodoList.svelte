<script>
  // @ts-nocheck

  const removeExpiredTodos = (todos) => {
    const now = new Date();
    return todos.filter((todo) => {
      if (!todo.expireAt) return true;
      return now < new Date(todo.expireAt);
    });
  };

  const getTodos = () => {
    if (!localStorage["todos"])
      return [{ id: 0, title: "Hello, World!", done: true }];

    const todos = JSON.parse(localStorage.getItem("todos")) || [];
    const actualTodos = removeExpiredTodos(todos);
    return actualTodos;
  };

  const saveTodos = (todos) => {
    localStorage.setItem("todos", JSON.stringify(todos));
  };

  let todos = getTodos();

  $: saveTodos(todos);

  const toggleTodo = (id) => {
    const todo = todos.find((unit) => unit.id === id);
    todo.done = !todo.done;

    if (todo.done) {
      const date = new Date();
      date.setDate(date.getDate() + 1);

      todo.expireAt = date;
    } else {
      delete todo.expireAt;
    }

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
