<template>
    <form @submit.prevent="addItem" class="item-add-form d-flex">
        <input v-model="itemName" type="text" class="form-control" placeholder="What needs to be done"/>
        <button class='btn btn-outline-secondary'>
            Add Item
        </button>
    </form>
</template>

<script lang="ts">
    import {Component, Prop, Vue} from 'vue-property-decorator';

    @Component({
        name: 'ItemAddForm',
    })
    export default class ItemAddForm extends Vue {

        public itemName: string = '';

        public addItem(): void {
            this.$emit('addItem', this.itemName);
            this.itemName = '';
        }
    }
</script>


<style>
    .item-add-form {
        margin: 0.5rem 0;
    }

    .item-add-form input {
        margin-right: 3px;
    }

    .item-add-form button {
        white-space: nowrap;
    }
</style>
