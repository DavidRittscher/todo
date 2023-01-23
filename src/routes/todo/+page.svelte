<script lang="ts">
    let newTodo = "";
    let whatsLeft = 0;
    let todoList = [
        { done: false, text: "Try to be positive!" },
        { done: false, text: "Brush your teeth." },
    ];

    $: whatsLeft = todoList.filter((t) => !t.done).length;
    function addNewTodo() {
        if (newTodo) {
            todoList = [...todoList, { done: false, text: newTodo }];
            newTodo = "";
            whatsLeft = todoList.filter((t) => !t.done).length;
        }
    }
    function removeTodo(index: number) {
        // todoList = todoList.filter((t, i) => i !== index);
        todoList.splice(index, 1);
        todoList = todoList;
        whatsLeft = todoList.filter((t) => !t.done).length;
    }
    function deleteLastTask(){
        todoList = todoList.slice(1);
    }
</script>

<h1 class="title">To-Do List</h1>
<div class="main-wrapper">
    <div class="header">
        <input
            class="startNewTodo"
            bind:value={newTodo}
            required={true}
            placeholder="Enter a task"
            on:keydown={(event) => {
                if (event.key === "Enter") {
                    addNewTodo();
                }
            }}
        />
        <button on:click={addNewTodo} disabled={!newTodo} class="addButton"
            >Add</button
        >
    </div>

    <div class="dropTodo">
        {#each todoList as todo, index}
            <!-- <div class:done={todo.done}> -->
            <label class="form-control">
                <input
                    id={`todo-${index}`}
                    class="todoInput"
                    type="checkbox"
                    bind:checked={todo.done}
                />

                <div class="todo-item">
                    <label
                        id="labelTodo"
                        class={todo.done ? "done" : ""}
                        for={`todo-${index}`}
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

                        <button
                            class="delete-icon"
                            on:click={() => removeTodo(index)}>❌</button
                        >
                    </label>
                </div>
            </label>
            <!-- </div> -->
        {/each}
    </div>
    <div class="endContainer">
        <div class="endBox">
            <p>{whatsLeft} Task{whatsLeft !==1 ? "s" : ""}</p>
        </div>
        <div class="hideBox">
            <button class="selectDelete" on:click={deleteLastTask}>❌</button>
        </div>
    </div>
</div>

<style>
    @media (min-width: 899px) {
        .header {
            width: auto;
            padding-left: 300px;
        }
    }

    .main-wrapper {
        display: flex;
        flex-direction: column;
        align-items: center;
        padding: 1rem;
        margin: 0 auto;
        min-width: 160px;
        max-width: 550px;
    }

    .header {
        display: flex;
        flex-wrap: nowrap;
        width: 100%;
        padding: 1rem;
        box-shadow: 0px 7px 12px 0px rgba(0, 0, 0, 0.25);
        margin: auto;
    }

    .startNewTodo {
        width: 90%;
        flex-grow: 1;
        padding: 0.5rem;
        background-color: #ffffff;
        color: var(--dark);
        border-style: solid;
        border-width: 1px;
        border-color: #cccccc;
        border-radius: 3px;
    }
    .startNewTodo:focus {
        outline-color: var(--dark);
        font-weight: bold;
        color: var(--dark);
    }
    .startNewTodo:focus::placeholder {
        color: transparent;
    }
    .addButton {
        padding: 0.45rem;
        margin-left: 0.2rem;
    }
    .dropTodo {
        width: 100%;
        display: flex;
        flex-direction: column;
        flex-wrap: wrap;
        padding-top: 0.6rem;
        padding-bottom: 0.6rem;
        padding-left: 1.3rem;
        border: 10px;
        box-shadow: 0px 7px 19px 2px rgba(0, 0, 0, 0.25);
    }
    .todo-item {
        flex-grow: 1;
        width: 90%;
        justify-content: space-between;
    }
    @media (min-width: 400px) {
        .delete-icon {
            visibility: hidden;
            border: none;
            background-color: var(--light);
            font-size: 0.8rem;
            float: right;
            /* transition: color 0.3s ease-out; */
            cursor: pointer;
        }
        .todo-item:hover .delete-icon {
            visibility: visible;
        }
    }
    .delete-icon {
        visibility: hidden;
    }
    input[type="checkbox"] {
        appearance: none;
        background-color: var(--light);
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
        box-shadow: inset 1em 1em var(--dark);
        background-color: var(--dark);
    }
    input[type="checkbox"]:checked::before {
        transform: scale(1);
    }
    #labelTodo.done {
        text-decoration: line-through;
        text-decoration-color: var(--dark);
    }

    .form-control {
        font-weight: bold;
        line-height: 1;
        display: grid;
        grid-template-columns: 1em auto;
        gap: 0.5em;
        margin-top: 1em;
    }
    .endContainer {
        display: flex;
        width: 100%;
        padding-top: 0.2rem;
        margin: auto;
        justify-content: space-between;
    }
    .endBox {
        padding: 0.5rem;
        box-shadow: 0px 7px 12px 0px rgba(0, 0, 0, 0.25);
        
    }
    .hideBox {
        visibility: hidden;
    }
    .selectDelete{
        border: none;
        background-color: inherit;
    }

    @media only screen and (max-width: 400px) {
        .hideBox {
            padding: 0.5rem;
            box-shadow: 3px 7px 12px 0px rgba(0, 0, 0, 0.25);
            visibility: visible;
        }
        .endBox {
            display: flex;
            box-shadow: -3px 7px 12px 0px rgba(0, 0, 0, 0.25);

            
        }
        .endBox p{
            content: " Task";
        }
    }
</style>
