<template>
    <div class="task-grid">
        <template v-if="this.tasks.length">
            <task v-for="task in tasks" :key="task.name" :task="task" 
                  @taskDeleted="$emit('taskDeleted',$event)"
                  @taskStateChanged="$emit('taskStateChanged', $event)"
            />
        </template>
        <p class="no-task" v-else>"Sua vida está em dia :)"</p>
    </div>
</template>

<script>
import Task from '@/components/Task.vue'

export default {
    components : {
        Task
    },
    props : {
        tasks : {type : Array, required : true} 
    }
}

</script>

<style>
    .task-grid {
        display: flex;
        flex-direction: row;
        justify-content: center;
        flex-wrap: wrap;
    }

    .no-task {
        color : #AAA;
        font-size : 1.7rem;
    }
</style>