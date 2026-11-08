<script lang="ts">
	let appTitle = 'My Todo List'
	
	let tasks = $state([
	  { id: crypto.randomUUID(), text: 'Learn Svelte', completed: false },
	  { id: crypto.randomUUID(), text: 'Build a todo app', completed: false },
	  { id: crypto.randomUUID(), text: 'Practice JS', completed: false }
	]);

	let newTask = $state('')

	function addNewTask() {
		if (newTask.trim() === '') {
			return
		}
		tasks.push({
			id: crypto.randomUUID(), text: newTask.trim(), completed: false
		})
		newTask = ''
	}

	function deleteTask(taskId: string) {
		tasks = tasks.filter(tasks => tasks.id !== taskId)
	}
</script>

<h1>{appTitle}</h1>

<input bind:value={newTask} placeholder="Enter a task" />
<button onclick={addNewTask}>
	Add Task
</button>

{#if tasks.length === 0}
	<p>No tasks yet!</p>
{/if}
<p>Total tasks: {tasks.length}</p>


{#each tasks as task (task.id)}
    <li>
        <label>
            <input bind:checked={task.completed} type="checkbox" />
            <span class:completed={task.completed}>{task.text}</span>
        </label>
        <button onclick={() => deleteTask(task.id)}>
            Delete
        </button>
    </li>
{/each}



<style>
	.completed{
		text-decoration: line-through
	}
</style>

