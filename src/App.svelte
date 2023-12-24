<script>
  let tasks = [];
  let newTask = '';

  const addTask = () => {
    if (newTask.trim() !== '') {
      tasks = [...tasks, { id: Date.now(), text: newTask, completed: false }];
      newTask = '';
    }
  };

  const removeTask = (taskId) => {
    tasks = tasks.filter(task => task.id !== taskId);
  };

  const toggleTask = (taskId) => {
    tasks = tasks.map(task =>
            task.id === taskId ? { ...task, completed: !task.completed } : task
    );
  };
</script>

<style>
  /* Ваши стили здесь */
</style>

<main>
  <h1>Todo List</h1>
  <input bind:value={newTask} placeholder="Добавить новую задачу" />
  <button on:click={addTask}>Добавить</button>

  {#if tasks.length > 0}
    <ul>
      {#each tasks as { id, text, completed }}
        <li class:completed={completed}>
          <input type="checkbox" bind:checked={completed} />
          <span>{text}</span>
          <button on:click={() => removeTask(id)}>Удалить</button>
        </li>
      {/each}
    </ul>
  {:else}
    <p>Список задач пуст.</p>
  {/if}
</main>
