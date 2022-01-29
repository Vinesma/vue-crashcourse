<template>
    <header>
        <h1>{{ title }}</h1>
        <Button
            v-show="homePage"
            @btn-click="toggleShowAddTask"
            :text="showAddTask ? 'Close' : 'Add Task'"
            :color="showAddTask ? 'red' : 'green'"
        />
    </header>
</template>

<script>
import Button from "./Button.vue";

export default {
    name: "Header",
    components: {
        Button,
    },
    props: {
        title: String,
        showAddTask: Boolean,
    },
    methods: {
        toggleShowAddTask() {
            this.$emit("toggle-show-add-task");
        },
    },
    computed: {
        homePage() {
            if (this.$route.path === "/") {
                return true;
            } else {
                return false;
            }
        },
    },
};
</script>

<style scoped>
header {
    display: flex;
    justify-content: space-between;
    align-items: center;
    margin-bottom: 20px;
}
</style>
