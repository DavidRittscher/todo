<script>
    // @ts-nocheck

    let todos = [
        { done: false, text: "Try not to cry over this." },
        { done: false, text: "Buy milk." },
    ];
    let newTodoText = "";
    $: remaining = todos.filter((t) => !t.done).length;
    function addNewTodo() {
        if (newTodoText) {
            todos = [...todos, { done: false, text: newTodoText }];
            newTodoText = "";
            remaining = todos.filter((t) => !t.done).length;
        }
    }
    function removeTodo(index) {
        todos = todos.filter((t, i) => i !== index)
        remaining = todos.filter((t) => !t.done).length;
    }
</script>

<h1 class="title">To-Do List</h1>
<body>
    <header class="header">
        <input
            class="startNewTodo"
            bind:value={newTodoText}
            required={true}
            placeholder="What needs to get done?"
            on:click={(event) => {}}
            on:keydown={(event) => {
                if (event.key === "Enter") {
                    addNewTodo();
                }
            }}
        />
        <button on:click={addNewTodo} disabled={!newTodoText} class="addButton"
            >Add</button
        >
    </header>
    <div class="dropTodo">
        {#each todos as todo, i}
            <div class:done={todo.done}>
                <label class="form-control">
                    <input
                        id={`todo-${i}`}
                        class="todoInput"
                        type="checkbox"
                        bind:checked={todo.done}
                    />

                    <div class="todo-item">
                        <label
                            id="labelTodo"
                            class={todo.done ? "done" : ""}
                            for={`todo-${i}`}
                            on:click={(event) => {
                                event.preventDefault();
                            }}
                            on:keydown={(event) => {
                                if (event.key === "Enter") {
                                    event.preventDefault();
                                }
                            }}
                        >
                            {todo.text}
                            <span
                                on:click={removeTodo}
                                on:keydown={(event) => {
                                    if (event.key === "Enter") {
                                        removeTodo();
                                    }
                                }}
                            />
                            <button class="delete-icon" on:click={() => removeTodo(i)}>x</button>
                        </label>
                    </div>
                </label>
            </div>
        {/each}
    </div>
    <div />
    <p>{remaining} Task to do</p>
</body>

<style>
    body {
        line-height: 1em;
        background: #f5f5f5;
        color: #4d4d4d;
        min-width: 14rem;
        max-width: 35rem;
        margin: 0 auto;
    }
    .title {
        font-family: system-ui, sans-serif;
        font-size: 6.25rem;
        font-weight: bold;
        text-shadow: 0.125rem 0.125rem 0.313rem rgba(99, 99, 99, 0.75);
        text-align: center;
        margin: auto;
        padding-bottom: 100px;
        margin-top: 6rem;
    }
    .header {
        align-content: center;
        padding-top: 1.5rem;
        padding-right: 1.5rem;
        padding-bottom: 1.2rem;
        padding-left: 3.75rem;
        box-shadow: 0px 7px 12px 0px rgba(0, 0, 0, 0.25);
    }
    .startNewTodo {
        padding: 0.313rem;
        padding-right: 6.25rem;
        font-family: system-ui, sans-serif;
        font-size: 1.5rem;
        background-color: #ffffff;
        color: #4d4d4d;
        border-style: solid;
        border-width: 1px;
        border-color: #cccccc;
        border-radius: 3px;

        width: 60%; /* set the width to be 100% of the parent element */
    }
    .startNewTodo:focus {
        outline-color: #4d4d4d;
        font-family: system-ui, sans-serif;
        font-weight: bold;
        width: 60%; /* set the width to be 100% of the parent element */
        color: #4d4d4d;
    }
    .startNewTodo:focus::placeholder {
        color: transparent;
    }
    .addButton {
        padding: 0.65rem;
        float: right;
        align-self: auto;
    }
    .delete-icon {
        display: none;
        border: none;
        float: right;
        margin: auto;
        padding-right: 3rem;
        background-color: #f5f5f5;
        font-size: 1.2rem;
        font-family: arial;
        color: #cc9a9a;
        transition: color 0.4s ease-out;
        cursor: pointer;
    }

    .todo-item:hover .delete-icon {
        display: inline-block;
    }
    .dropTodo {
        padding-top: 0.313rem;
        padding-bottom: 1rem;
        padding-left: 0.8rem;
        border: 10px;
        box-shadow: 0px 7px 19px 2px rgba(0, 0, 0, 0.25);
    }

    #labelTodo {
        padding-left: 1.6rem;
    }
    input[type="checkbox"] {
        appearance: none;
        background-color: #f5f5f5;
        margin: 0;
        font: inherit;
        color: currentColor;
        width: 1.15em;
        height: 1.15em;
        border: 0.15em solid currentColor;
        border-radius: 0.15em;
        transform: translateY(-0.075em);
        display: grid;
        place-content: center;
    }
    input[type="checkbox"]::before {
        content: "";
        width: 0.65em;
        height: 0.65em;
        transform: scale(0);
        transition: 120ms transform ease-in-out;
        box-shadow: inset 1em 1em var(--form-control-color);
        background-color: #4d4d4d;
    }
    input[type="checkbox"]:checked::before {
        transform: scale(1);
    }
    #labelTodo.done {
        text-decoration: line-through;
        text-decoration-color: #4d4d4d;
    }

    .form-control {
        font-family: system-ui, sans-serif;
        font-size: 1.5rem;
        font-weight: bold;
        line-height: 1.1;
        display: grid;
        grid-template-columns: 1em auto;
        gap: 0.5em;
        margin-top: 0.75em;
    }
</style>
