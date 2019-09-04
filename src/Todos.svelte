<script>
    import TodoItem from './TodoItem.svelte';

    let newTodoTitle = '';
    let currentFilter = 'all';
    let nextId = 4;
    let todos = [
        {
            id: 1,
            title: 'Mi primera tarea',
            completed: false
        },
        {
            id: 2,
            title: 'Mi segunda tarea',
            completed: false
        },
        {
            id: 3,
            title: 'Mi tercera tarea',
            completed: false
        }
    ];

    function addTodo(event) {
        if(event.key === 'Enter') {
            todos = [...todos, {
                id: nextId,
                title: newTodoTitle,
                completed: false
            }];

            nextId += 1;
            newTodoTitle = '';
        }
    }
    function checkAllTodos() {
        todos.forEach(todo => todo.completed = event.target.checked);
        todos = todos;
    }
    function updateFilter(newFilter) {
        currentFilter = newFilter;
    }
    function clearCompleted() {
        todos = todos.filter(todo => !todo.completed);
    }
    function handleDeleteTodo(event) {
        todos = todos.filter(todo => todo.id !== event.detail.id);
    }
    function handleToggleComplete(event) {
        const todoIndex = todos.findIndex(todo => todo.id === event.detail.id);
        const updatedTodo = {...todos[todoIndex], completed: !todos[todoIndex].completed};
        todos = [...todos.slice(0, todoIndex), updatedTodo, ...todos.slice(todoIndex + 1)];
    }

    $: todosRemaining = filteredTodos.filter(todo => !todo.completed).length;
    $: filteredTodos = currentFilter === 'all' ? todos : currentFilter === 'completed' ? todos.filter(todo => todo.completed) : todos.filter(todo => !todo.completed);

</script>

<style>
    .container {
        max-width: 800px;
        margin: 10px auto;
    }
    .logo {
        display: block;
        margin: 20px auto;
        width: 40%;
    }
    .todo-input {
        width: 100%;
        padding: 10px, 20px;
        font-size: 18px;
        margin-bottom: 20px;
    }
    .inner-container {
        display: flex;
        align-items: center;
        justify-content: space-between;
        font-size: 16px;
        border-top: 1px solid lightgrey;
        padding-top: 15px;
        margin-bottom: 13px;
    }
    .inner-container-input {
        margin-right: 12px;
    }
    button {
        font-size: 14px;
        background-color: white;
        appearance: none;
    }
    button:hover {
        background: lightseagreen;
    }
    button:focus {
        outline: none;
    }
    .active {
        background: lightseagreen;
    }
</style>

<div class="container">
    <a href="https://github.com/vicentbg" target="_blank"><img src={'https://fireship.io/lessons/svelte-v3-overview-firebase/img/featured.png'} alt="yo logo" class="logo"></a>

    <span style="font-size: 48px; color: Dodgerblue;">
        <i class="fas fa-clipboard-list"></i>
    </span>
    <h2>Svelte ToDo App </h2>
    
    <input type="text" class="todo-input" placeholder="Introduce nueva tarea..." bind:value={newTodoTitle} on:keydown={addTodo}>

    {#each filteredTodos as todo}
        <div class="todo-item">
            <TodoItem {...todo} on:deleteTodo={handleDeleteTodo} on:toggleComplete={handleToggleComplete} />
        </div>
    {/each}

    <div class="inner-container">
        <div><label><input type="checkbox" class="inner-container-input" on:change={checkAllTodos}>Marcar Todos</label></div>
        <div>{todosRemaining} tareas pendientes</div>
    </div>

    <div class="inner-container">
        <div>
            <button on:click={() => updateFilter('all')} class:active="{currentFilter === 'all'}">Todos</button>
            <button on:click={() => updateFilter('active')} class:active="{currentFilter === 'active'}">Pendientes</button>
            <button on:click={() => updateFilter('completed')} class:active="{currentFilter === 'completed'}">Completados</button>
        </div>

        <div>
            <button on:click={clearCompleted}>Borrar Completados</button>
        </div>
    </div>
</div>