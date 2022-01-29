<template>
    <ol>
        <Task
            @delete-task="$emit('delete-task', task.id)"
            @toggle-reminder="$emit('toggle-reminder', task.id)"
            v-for="task in tasks"
            :key="task.id"
            :task="task"
        />
    </ol>
</template>

<script>
import Task from "./Task.vue";

export default {
    name: "Tasks",
    components: {
        Task,
    },
    props: {
        tasks: Array,
    },
    emits: ["delete-task", "toggle-reminder"],
};
</script>
