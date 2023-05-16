<script>
    import { onMount } from "svelte";
    import { browser } from "$app/environment";

    let todoText = "";
    let todos = [];

    onMount(() => {
        if (browser) {
            const storedTodos = JSON.parse(localStorage.getItem("todos"));
            if (storedTodos) {
                todos = storedTodos;
            }
        }
    });

    function saveTodos() {
        // Save todos to local storage
        if (browser) {
            localStorage.setItem("todos", JSON.stringify(todos));
        }
    }

    function addTodo() {
        todos.push({ text: todoText, done: false }); //objekt
        todos = todos;
        todoText = ""; //每次点击ADD按钮时会清空输入栏
        console.log(todos);
    }

    function remove(index) {
        todos.splice(index, 1);
        todos = todos;
    }
    () => {};
    function handleKeyDown(event) {
    if (event.keyCode === 13) {
        addTodo();
    }
}

</script>

<link rel="preconnect" href="https://fonts.googleapis.com" />
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin />
<link
    href="https://fonts.googleapis.com/css2?family=Parisienne&family=Special+Elite&display=swap"
    rel="stylesheet"
/>
<body>
    <div class="background-container">
        <div class="overlay">
            <h1>TODO APP</h1>

            <div class="input-container">
                <input type="text" class="todo-input" bind:value={todoText} on:keydown={handleKeyDown} />
                <button class="add-button" on:click={addTodo}>
                    <svg
                        width="24"
                        height="24"
                        viewBox="0 0 24 24"
                        xmlns="http://www.w3.org/2000/svg"
                    >
                        <title />

                        <g id="Complete">
                            <g data-name="add" id="add-2">
                                <g>
                                    <line
                                        fill="none"
                                        stroke="#000000"
                                        stroke-linecap="round"
                                        stroke-linejoin="round"
                                        stroke-width="2"
                                        x1="12"
                                        x2="12"
                                        y1="19"
                                        y2="5"
                                    />

                                    <line
                                        fill="none"
                                        stroke="#000000"
                                        stroke-linecap="round"
                                        stroke-linejoin="round"
                                        stroke-width="2"
                                        x1="5"
                                        x2="19"
                                        y1="12"
                                        y2="12"
                                    />
                                </g>
                            </g>
                        </g>
                    </svg>
                </button>
            </div>

            <!-- todo -->
            {#each todos as todo}
                <div class="todo-entry" class:done={todo.done}>
                    <div class="todo-text">{todo.text}</div>
                    <input type="checkbox" bind:value={todo.done} />
                    <button
                        class="delete"
                        on:click={(index) => {
                            remove(index);
                        }}
                    >
                        <svg
                            xmlns="http://www.w3.org/2000/svg"
                            width="24"
                            height="24"
                            viewBox="0 0 1024 1024"
                            fill="black"
                            class="icon"
                            version="1.1"
                        >
                            <path
                                d="M32 241.6c-11.2 0-20-8.8-20-20s8.8-20 20-20l940 1.6c11.2 0 20 8.8 20 20s-8.8 20-20 20L32 241.6zM186.4 282.4c0-11.2 8.8-20 20-20s20 8.8 20 20v688.8l585.6-6.4V289.6c0-11.2 8.8-20 20-20s20 8.8 20 20v716.8l-666.4 7.2V282.4z"
                            />
                            <path
                                d="M682.4 867.2c-11.2 0-20-8.8-20-20V372c0-11.2 8.8-20 20-20s20 8.8 20 20v475.2c0.8 11.2-8.8 20-20 20zM367.2 867.2c-11.2 0-20-8.8-20-20V372c0-11.2 8.8-20 20-20s20 8.8 20 20v475.2c0.8 11.2-8.8 20-20 20zM524.8 867.2c-11.2 0-20-8.8-20-20V372c0-11.2 8.8-20 20-20s20 8.8 20 20v475.2c0.8 11.2-8.8 20-20 20zM655.2 213.6v-48.8c0-17.6-14.4-32-32-32H418.4c-18.4 0-32 14.4-32 32.8V208h-40v-42.4c0-40 32.8-72.8 72.8-72.8H624c40 0 72.8 32.8 72.8 72.8v48.8h-41.6z"
                            />
                        </svg>
                    </button>
                </div>
            {/each}
        </div>
    </div>
</body>

<style>
    * {
        margin: 0;
        padding: 0;
        box-sizing: border-box;
        font-family: "Special Elite", cursive;
    }

    body {
        background-image: url("schwarzMuster.jpeg");
        background-color: #f4f4f4;
        background-position: center;
        background-repeat: no-repeat;
        display: flex;
        justify-content: center;
        align-items: center;
        height: 100vh;
    }

    .background-container {
        position: relative;
    }

    .overlay {
        position: absolute;
        top: 50%;
        left: 50%;
        transform: translate(-50%, -50%);
        background-color: white;
        padding: 20px;
        display: flex;
        flex-direction: column;
        align-items: center;
        border: 2px solid black;
    }

    h1 {
        font-family: "Special Elite", cursive;
        text-align: center;
        margin-bottom: 20px;
    }

    .input-container {
        display: flex;
        gap: 10px;
        margin-bottom: 20px;
    }

    .todo-input {
        flex-grow: 1;
        padding: 10px;
        border: 2px solid black;
        border-radius: 4px;
    }

    .add-button {
        background-color: white;
        border: none;
        padding: 8px;
        cursor: pointer;
    }

    .delete {
        background-color: white;
        border: none;
        padding: 6px;
        cursor: pointer;
    }

    .done {
        color: grey;
    }

    .todo-entry {
        display: flex;
    align-items: center;
    }

    .todo-text {
        flex-grow: 1;
    }

    .todo-entry.done .todo-text {
        text-decoration: line-through;

    }

    .todo-entry input[type="checkbox"] {
        margin-left: 10px;
        margin-right: 3px;
    }

    .checkbox-label {
        width: 16px;
        height: 16px;
        border: 2px solid black;
        display: inline-block;
        margin-right: 6px;
        cursor: pointer;
    }

    .checkbox-label::after {
        content: "";
        display: block;
        width: 10px;
        height: 10px;
        background-color: black;
        opacity: 0;
        transition: opacity 0.2s;
    }

    .todo-entry.done .checkbox-label::after {
        opacity: 1;
    }
</style>
