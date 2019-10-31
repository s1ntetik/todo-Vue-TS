<template>
    <div class="btn-group">
        <button type="button"
                class="btn"
                value="all"
                @click="changeFilter"
                :class="{
				'btn-info': filter === 'all',
				'btn-outline-secondary': filter !== 'all' }"
        >
            All
        </button>
        <button type="button"
                class="btn"
                value="active"
                @click="changeFilter"
                :class="{
				'btn-info': filter === 'active',
				'btn-outline-secondary': filter !== 'active' }"
        >
            Active
        </button>
        <button type="button"
                class="btn"
                value="done"
                @click="changeFilter"
                :class="{
				'btn-info': filter === 'done',
				'btn-outline-secondary': filter !== 'done' }"
        >
            Done
        </button>
    </div>
</template>

<script lang="ts">
    import {Component, Prop, Vue} from 'vue-property-decorator';

    @Component({
        name: 'ItemStatusFilter',
    })
    export default class ItemStatusFilter extends Vue {
        @Prop(String) public filter: string = 'all';

        public changeFilter(event: MouseEvent): void {
            this.$emit('filter', (event.target as HTMLInputElement).value);
        }
    }
</script>

<style>

</style>
