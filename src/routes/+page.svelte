<script lang="ts">
	import TodoForm from "#lib/components/TodoForm.svelte";
	import type { Task } from "#lib/types.ts";
	import TodoItem from "../lib/components/TodoItem.svelte";

	let appTitle = 'My Todo List'

	let tasks = $state<Task[]>([
	  { id: crypto.randomUUID(), text: 'Learn Svelte', completed: false },
	  { id: crypto.randomUUID(), text: 'Build a todo app', completed: false },
	  { id: crypto.randomUUID(), text: 'Practice JS', completed: false }
	]);

	// let newTask = $state('')
    let filter = $state('all')

    let filteredTasks = $derived(
        tasks.filter(task => {
            if(filter === 'active') {
                return !task.completed
            } else if(filter === 'completed') {
                return task.completed
            } else {
                return true
            }
        })
    )

	function addNewTask(task: string) {
		if (task.trim() === '') {
			return
		}
		tasks.push({
			id: crypto.randomUUID(), text: task.trim(), completed: false
		})
	}

	function deleteTask(taskId: string) {
		tasks = tasks.filter(tasks => tasks.id !== taskId)
	}

    function toggleTask(task: Task) {
        task.completed = !task.completed
    }

</script>

<h1>{appTitle}</h1>


<TodoForm onAddTask={addNewTask}/>

{#if tasks.length === 0}
	<p>No tasks yet!</p>
{/if}
<p>Total tasks: {tasks.length}</p>

<button onclick={() => filter = 'active'}>Active</button>
<button onclick={() => filter = 'completed'}>Completed</button>
<button onclick={() => filter = 'all'}>All</button>



{#each filteredTasks as task (task.id)}
 <TodoItem task={task} onToggle={()=> toggleTask(task)} onDelete={()=>deleteTask(task.id)}/>  
{/each}

