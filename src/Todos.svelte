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

<h2>Svelte ToDo App</h2>
<input type="text" class="todo-input" placeholder="Introduce nueva tarea..." bind:value={newTodoTitle} on:keydown={addTodo}>
