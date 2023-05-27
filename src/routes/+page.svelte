<script>
    let todos = [];
    let task = '';

    const addTodo = () => {
        let todo = {
            task: task,
            isComplete: false,
            createdAt: new Date(),
        };
        todos = [todo, ...todos];
        task = "";
    };

    const markTodoAsComplete = (index) => {
        todos[index].isComplete = !todos[index].isComplete;
    };

    const deleteTodo = (index) => {
        let deleteItem = todos[index];
        todos = todos.filter((item) => item !== deleteItem);
    };
    $: console.table(todos);
</script>

<style>
    .container {
        max-width: 600px;
        margin: 20px auto;
        padding: 60px;
        background-color: #fff;
        box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
        border-radius: 5px;
    }

    h1 {
        text-align: center;
        color: #333;
    }

    input[type="text"] {
        width: 100%;
        padding: 10px;
        border: 1px solid #ccc;
        border-radius: 4px;
        font-size: 16px;
    }

    button {
        padding: 10px 15px;
        font-size: 16px;
        color: #fff;
        background-color: #4CAF50;
        border: none;
        border-radius: 4px;
        cursor: pointer;
        margin-top: 10px;
    }

    button:hover {
        background-color: #45a049;
    }

    ol {
        list-style-type: none;
        padding: 0;
    }

    li {
        display: flex;
        align-items: center;
        justify-content: space-between;
        padding: 10px;
        border-bottom: 1px solid #ccc;
    }

    li.complete {
        text-decoration: line-through;
        color: #999;
    }

    .todoitem {
        flex-grow: 1;
    }

    .buttons {
        display: flex;
        align-items: center;
    }

    .buttons button {
        padding: 6px 12px;
        margin-left: 5px;
        font-size: 20px;
        color: #fff;
        background-color: #ffffff;
        border: none;
        border-radius: 3px;
        cursor: pointer;
    }

    .buttons button:first-child {
        background-color: #ffffff;
    }

    .buttons button:hover {
        opacity: 0.8;
    }
</style>

<div class="container">
    <h1>Todo App</h1>

    <input type="text" placeholder="Add a task" bind:value={task} />
    <button on:click={addTodo}>Add</button>

    <ol>
        {#each todos as item, index}
        <li class:complete={item.isComplete}>
            <div class="todoitem">
                <span>{item.task}</span>
            </div>
            <span class="buttons">
                <button on:click={() => markTodoAsComplete(index)}>✅</button>
                <button on:click={() => deleteTodo(index)}>❎</button>
            </span>
        </li>
        {/each}
    </ol>
</div>