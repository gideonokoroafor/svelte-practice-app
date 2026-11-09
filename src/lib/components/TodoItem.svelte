<script lang="ts">
	import type { Task } from "#lib/types.ts";

    
    let { task,  onToggle, onDelete } : {
        task: Task
        onToggle: () => void
        onDelete: () => void
    } = $props()
    
</script>

<article>
    <label>
        <input type="checkbox" checked={task.completed} onchange={onToggle}/>
        <span class:completed={task.completed}>{task.text}</span>
    </label>
    <button onclick={onDelete}>
        Delete
    </button>
</article>

<style>
	.completed{
		text-decoration: line-through
	}
</style>