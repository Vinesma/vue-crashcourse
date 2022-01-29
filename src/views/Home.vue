<template>
    <AddTask v-show="showAddTask" @add-task="addTask" />
    <Tasks
        @delete-task="deleteTask"
        @toggle-reminder="toggleReminder"
        :tasks="tasks"
    />
</template>

<script>
import Tasks from "../components/Tasks.vue";
import AddTask from "../components/AddTask.vue";

export default {
    name: "Home",
    components: {
        Tasks,
        AddTask,
    },
    props: {
        showAddTask: Boolean,
    },
    data() {
        return {
            tasks: [],
            api: "api/tasks",
        };
    },
    methods: {
        async fetchTasks() {
            const response = await fetch(this.api);
            this.tasks = await response.json();
        },
        async addTask(task) {
            try {
                const response = await fetch(this.api, {
                    method: "POST",
                    headers: {
                        "Content-Type": "application/json",
                    },
                    body: JSON.stringify(task),
                });
                const newTask = await response.json();

                this.tasks = [...this.tasks, newTask];
            } catch (error) {
                console.error(error);
            }
        },
        async deleteTask(id) {
            if (confirm("Are you sure you want to delete this task?")) {
                try {
                    await fetch(`${this.api}/${id}`, { method: "DELETE" });
                    this.tasks = this.tasks.filter(task => task.id !== id);
                } catch (error) {
                    console.error(error);
                }
            }
        },
        async toggleReminder(id) {
            const task = this.tasks.filter(task => task.id === id)[0];
            const updatedTask = { ...task, reminder: !task.reminder };

            try {
                await fetch(`${this.api}/${id}`, {
                    method: "PUT",
                    headers: {
                        "Content-Type": "application/json",
                    },
                    body: JSON.stringify(updatedTask),
                });

                this.tasks = this.tasks.map(task =>
                    task.id === id ? updatedTask : task
                );
            } catch (error) {
                console.error(error);
            }
        },
    },
    created() {
        this.fetchTasks();
    },
};
</script>
