<script>
    let todoText = '';
    let todos = [];
    let deletedTodos = [];

    function saveTodoList(todoList) {
                localStorage.setItem('todoList', JSON.stringify(todoList));
        }
        function getTodoList() {
                const todoList = localStorage.getItem('todoList');
                return todoList ? JSON.parse(todoList) : [];
        }

    function addTodo() {
        todos.push({text: todoText, done: false});
        todos = todos;
        todoText = '';
    }

    function remove(index) {
        const deletedTodo = todos.splice(index, 1)[0];
        deletedTodos.push(deletedTodo);
        todos = todos;
        saveTodoList(todos);
    }

    function clearAllTodos() {
        todos = [];
        saveTodoList(todos);
    }

</script>

<h1>TODO APP</h1>

<!--textfeld-->
<input type="text" class="todo-input" bind:value={todoText}/>

<!--button add-->
<button id="add" on:click={addTodo}>ADD</button>

<!--todo-->
{#each todos as todo, index}
    <div class="todo-entry" class:done={todo.done}>
        <div>{todo.text}</div>
        <input type="checkbox" bind:value={todo.done}/>
        <button class="delete" on:click={remove}>X</button>
    </div>
{/each}

<button on:click={clearAllTodos}>Clear All</button>


<h2>Deleted Items</h2>
<!--deleted todos: Eigentlich sollten hier die gelöschten todos aufgelistet werden, aber das klappt irgendwie nicht:/-->
{#each deletedTodos as todo}
    <div class="deleted-entry">
        <div>{todo.text}</div>
    </div>
{/each}
<!--text-->
<!--checkboxen-->
<style>
    h1, h2, .todo-entry{
        font-family: sans-serif
    }

    .todo-input {
        padding: 10px;
        margin-bottom: 10px;
        font-size: 16px;
        border-radius: 4px;
        border: 1px solid #ccc;
    }

    .todo-entry {
        width: 10%;
        background-color: #fff;
        padding: 10px;
        margin-bottom: 10px;
        border-radius: 4px;
        box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
    }

    .todo-entry.done {
        opacity: 0.5;
    }

    .delete {
        background-color: white;
        border: none;
    }

    .delete:hover {
        background-color: orange;
    }

    .delete:active {
        background-color: red;
    }
    .done {
        color: grey;
    }
    .todo-entry {
        display: flex;
    }
    .deleted-entry {
        color: red;
    }
    
</style>
