<template>
    <li
        :class="[task.reminder ? 'reminder' : '', 'task']"
        @dblclick="$emit('toggle-reminder', task.id)"
    >
        <h3>
            {{ task.text }}
            <div @click="onDelete(task.id)" class="delete-icon"></div>
        </h3>
        <p>{{ task.day }}</p>
    </li>
</template>

<script>
export default {
    name: "Task",
    methods: {
        onDelete(id) {
            this.$emit("delete-task", id);
        },
    },
    props: {
        task: Object,
    },
};
</script>

<style scoped>
.fas {
    color: red;
}
.task {
    background: #f4f4f4;
    margin: 5px;
    padding: 10px 20px;
    cursor: pointer;
}
.task.reminder {
    border-left: 5px solid green;
}
.task h3 {
    display: flex;
    align-items: center;
    justify-content: space-between;
}
.task h3,
.task p {
    pointer-events: none;
}
.delete-icon {
    position: relative;
    width: 16px;
    height: 16px;
    pointer-events: all;
}
.delete-icon:after {
    content: "";
    position: absolute;
    top: 0;
    width: 4px;
    height: 100%;
    background-color: red;
    transform: rotate(-45deg);
    border-radius: 4px;
}
.delete-icon:before {
    content: "";
    position: absolute;
    top: 0;
    width: 4px;
    height: 100%;
    background-color: red;
    transform: rotate(45deg);
    border-radius: 4px;
}
</style>
