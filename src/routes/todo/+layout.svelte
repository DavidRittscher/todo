<script lang="ts">
    export let newTodo = "";
    export let whatsLeft = 0;
    export let todoList = [
        { done: false, text: "Try to be positive!" },
        { done: false, text: "Brush your teeth." },
    ];

    $: whatsLeft = todoList.filter((t) => !t.done).length;
    export function addNewTodo() {
        if (newTodo) {
            todoList = [...todoList, { done: false, text: newTodo }];
            newTodo = "";
            whatsLeft = todoList.filter((t) => !t.done).length;
        }
    }
    export function removeTodo(index: number) {
        // todoList = todoList.filter((t, i) => i !== index);
        todoList.splice(index, 1);
        todoList = todoList;
        whatsLeft = todoList.filter((t) => !t.done).length;
    }
</script>

<slot />
