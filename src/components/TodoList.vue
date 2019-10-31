<template>
    <ul class="list-group todo-list">
        <li v-for="item in todoData" :key="item.id" class="list-group-item">
            <todo-list-item :item="item" @toParentEvent="toParentEvent"/>
        </li>
    </ul>
</template>

<script lang="ts">
    import TodoListItem from '@/components/TodoListItem.vue';
    import { Component, Prop, Vue } from 'vue-property-decorator';

    @Component({
        name: 'TodoList',
        components: {
            TodoListItem
        },
    })
    export default class TodoList extends Vue {
        @Prop({ type: Array, required: true }) public todoData!: [];

        public toParentEvent(id: number, nameProps: string): void {
            this.$emit('toParentEvent', id, nameProps)
        }
    }
</script>


<style>
    .todo-list .list-group-item {
        padding: .25rem .75rem;
    }
</style>
