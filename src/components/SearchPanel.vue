<template>
    <input
            v-model="searchInput"
            type="text"
            class="form-control search-input"
            @input="onSearch"
            placeholder="type to search"/>
</template>

<script lang="ts">
    import {Component, Prop, Vue} from 'vue-property-decorator';

    @Component({
        name: 'SearchPanel',
    })
    export default class SearchPanel extends Vue {

        public searchInput: string = '';

        public onSearch(): void {
            this.$emit('onSearch', this.searchInput);
        }
    }
</script>

<style>
    .search-input {
        width: auto;
        flex-grow: 1;
        margin-right: 3px;
    }

</style>
