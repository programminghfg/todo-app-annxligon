<script>
    let todoText = '';
    let todos = [];

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
        todos.splice(index, 1);
        todos = todos;
    }

</script>

<h1>TODO APP</h1>

<!--textfeld-->
<input type="text" class="todo-input" bind:value={todoText}/>

<!--button add-->
<button on:click={addTodo}>ADD</button>

<!--todo-->
{#each todos as todo, index}
    <div class="todo-entry" class:done={todo.done}>
        <div>{todo.text}</div>
        <input type="checkbox" bind:value={todo.done}/>
        <button class="delete" on:click={remove}>X</button>
    </div>
{/each}
<!--text-->
<!--checkboxen-->
<style>
    .delete {
        background-color: white;
        border: none;
    }

    .delete:hover {
        background-color: orange;
    }
    .done {
        color: grey;
    }
    .todo-entry {
        display: flex;
    }
</style>