<script lang="ts">

    let newTask = $state('')
    let {onAddTask} : {
        onAddTask: (newTask: string) => void
    } = $props()

    function addTask(e: SubmitEvent){
        e.preventDefault()
        const text = newTask.trim()
        if(!text) return
        onAddTask(text);
        newTask = ""
    }

</script>

<form onsubmit={addTask}>
   <input bind:value={newTask} placeholder="Enter a task" />
    <button type="submit">
        Add Task
    </button>
</form>