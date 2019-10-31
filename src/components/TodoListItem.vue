<template>
    <span
            class="todo-list-item"
            :class="getClassName"
    >
      <span class="todo-list-item-label"
            @click="toParentEvent('done')"
      >
        {{item.label}}
      </span>

      <button type="button" class="btn btn-outline-success btn-sm float-right" @click="toParentEvent('important')">
        <i class="fa fa-exclamation"/>
      </button>

      <button type="button" class="btn btn-outline-danger btn-sm float-right" @click="toParentEvent('delete')">
        <i class="fa fa-trash-o"/>
      </button>
    </span>
</template>

<script lang="ts">
    import {ITodoItem} from '@/interfaces/interface';
    import {Component, Prop, Vue} from 'vue-property-decorator';

    @Component({
        name: 'TodoListItem',
    })
    export default class TodoListItem extends Vue {
        @Prop(Object) public item!: ITodoItem;

        get getClassName(): any {
            return {
                done: this.item.done,
                important: this.item.important
            };
        }

        public toParentEvent(nameProps: string): void {
            this.$emit('toParentEvent', this.item.id, nameProps);
        }
    }
</script>


<style>
    .todo-list-item {
        font-size: 1.25rem;
    }

    .todo-list-item button {
        width: 35px;
        margin: 3px;
    }

    .todo-list-item-label {
        margin-left: 1.25rem;
        line-height: 35px;
        cursor: pointer;
        user-select: none;
    }

    .todo-list-item.done .todo-list-item-label {
        text-decoration: line-through;
    }

    .todo-list-item.important .todo-list-item-label {
        font-weight: bold;
        color: steelblue;
    }
</style>
