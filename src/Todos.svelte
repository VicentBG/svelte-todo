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
</script>

<div class="container">
    <h2>Svelte ToDo App</h2>
    <input type="text" class="todo-input" placeholder="Introduce nueva tarea..." bind:value={newTodoTitle} on:keydown={addTodo}>

    {#each filteredTodos as todo}
        <div class="todo-item">
            <TodoItem {...todo} on:deleteTodo={handleDeleteTodo} on:toggleComplete={handleToggleComplete} />
        </div>
    {/each}

    <div class="inner-container">
        <div><label><input type="checkbox" class="inner-container-input" on:change={changeAllTodos}>Marcar Todos</label></div>
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