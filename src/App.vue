<template>
    <div class="todo-app">
        <app-header :count="todoCount"/>
        <div class="top-panel d-flex">
            <search-panel @onSearch="onSearch"/>
            <item-status-filter :filter="filter" @filter="onFilter"/>
        </div>
        <todo-list :todoData="visibleItems" @toParentEvent="onGetEvent"/>
        <item-add-form @addItem="addItem"/>
    </div>
</template>

<script lang="ts">
    import AppHeader from '@/components/AppHeader.vue';
    import ItemAddForm from '@/components/ItemAddForm.vue';
    import ItemStatusFilter from '@/components/ItemStatusFilter.vue';
    import SearchPanel from '@/components/SearchPanel.vue';
    import TodoList from '@/components/TodoList.vue';
    import {ITodoItem} from '@/interfaces/interface';
    import {Component, Vue} from 'vue-property-decorator';

    @Component({
        name: 'App',
        components: {
            ItemAddForm,
            TodoList,
            ItemStatusFilter,
            AppHeader,
            SearchPanel,
        },
    })

    export default class App extends Vue {

        public todoData: any = [];
        public itemId: number = 0;
        public filter: string = 'all';
        public searchText: string = '';

        public mounted(): void {
            this.todoData = [
                this.createTodoItem('Drink Coffee'),
                this.createTodoItem('Learn TypeScript'),
                this.createTodoItem('Break'),
            ];
        }

        public createTodoItem(label: string): ITodoItem {
            return {
                label,
                important: false,
                done: false,
                id: this.itemId++
            };
        }

        public addItem(itemName: string): void {
            const newItem: ITodoItem = this.createTodoItem(itemName);
            this.$set(this.todoData, this.todoData.length++, newItem);
        }

        public onGetEvent(id: number, nameProps: string): void {
            const idx: number = this.todoData.findIndex((item: ITodoItem) => item.id === id);

            if (nameProps === 'delete') {
                this.$delete(this.todoData, idx);
            } else {
                this.todoData[idx][nameProps] = !this.todoData[idx][nameProps];
            }
        }

        public onFilter(value: string): void {
            this.filter = value;
        }

        public onSearch(searchText: string): void {
            this.searchText = searchText;
        }

        public filterItems(items: ITodoItem[], filter: string): ITodoItem[] {
            switch (filter) {
                case 'all':
                    return items;
                case 'active':
                    return items.filter((item: ITodoItem) => !item.done);
                case 'done':
                    return items.filter((item: ITodoItem) => item.done);
                default:
                    return items;
            }
        }

        public get visibleItems(): ITodoItem[] {
            const visibleItems: ITodoItem[] = this.todoData.filter((item: ITodoItem) => {
                return item.label.toLowerCase().indexOf(this.searchText.toLowerCase()) > -1;
            });

            const filterItems: ITodoItem[] = this.filterItems(visibleItems, this.filter);
            return filterItems;
        }

        public get todoCount(): {} {
            const doneCount: number = this.todoData.filter((el: ITodoItem) => el.done).length;
            const todoCount: number = this.todoData.length - doneCount;

            return {
                todoCount,
                doneCount
            };
        }

    }
</script>

<style lang="scss">
    .todo-app {
        margin: 2rem auto 0 auto;
        max-width: 400px;
    }

    .top-panel {
        margin: 1rem 0;
    }
</style>
