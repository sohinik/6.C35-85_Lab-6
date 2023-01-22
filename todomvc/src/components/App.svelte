<script>
    import ToDo from '../components/ToDo.svelte';

    let placeholder = "What do you need to do?";
    let todo_text = "";

    let todos = [
        { id: "0", text: "Learn Svelte", completed: false },
        { id: "1", text: "Finish Lab", completed: false },
    ];

    let next_id = 2;

    function add() {
        todos = todos.concat({
            id: next_id,
            text: todo_text,
            completed: false,
        });
        next_id = next_id + 1;
        todo_text = "";
    }
</script>

<main>
    <h1>todos</h1>

    <section class="todos">
        <form on:submit|preventDefault={add}>
            <input {placeholder} bind:value={todo_text} />
        </form>

        {#each todos as todo (todo.id)}
            <ToDo bind:todo={todo} />
        {/each}

        <div class="actions" />
    </section>
</main>

<style>
    @import url("https://fonts.googleapis.com/css2?family=Nunito:wght@300;400;700&display=swap");

    :root {
        --color-bg: #f7f7f7;
        --color-outline: #c2c2c2;
        --color-shadow: hsl(0, 0%, 0%, 0.1);
        --color-text: #222222;
        --color-bg-1: hsla(0, 0%, 0%, 0.2);
        --color-shadow-1: hsl(0, 0%, 96%);
    }

    *,
    *::before,
    *::after {
        margin: 0;
        padding: 0;
        box-sizing: border-box;
    }

    main {
        height: 100%;
        display: grid;
        place-content: center;
        text-align: center;
        font-family: "Nunito", sans-serif;
        font-weight: 300;
        line-height: 2;
        font-size: 24px;
        color: var(--color-text);
    }

    label,
    input,
    button {
        font-family: inherit;
        font-weight: inherit;
        line-height: inherit;
        font-size: 24px;
        width: 100%;
    }

    h1 {
        font-size: 72px;
        font-weight: 300;
        line-height: 1.4;
    }

    .todos {
        width: 500px;
        background-color: var(--color-bg);
        border-radius: 5px;
        border: 1px solid var(--color-outline);
        box-shadow: 0 0 4px var(--color-shadow);
    }

    /* .actions {
        position: relative;
        display: flex;
        align-items: center;
        justify-content: space-between;
    }
    .actions:before {
        content: "";
        height: 40px;
        position: absolute;
        right: 0;
        bottom: 0;
        left: 0;
        box-shadow: 0 1px 1px var(--color-shadow-1), 0 8px 0 -3px var(--color-shadow-1),
            0 9px 1px -3px var(--color-bg-1), 0 16px 0 -6px var(--color-shadow-1),
            0 17px 2px -6px var(--color-bg-1);
        z-index: -1;
    } */
</style>
