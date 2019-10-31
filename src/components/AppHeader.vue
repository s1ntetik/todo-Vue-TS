<template>
    <div class="app-header d-flex">
        <h1>Todo List</h1>
        <h2>{{ count.todoCount }} more to do, {{ count.doneCount }} done</h2>
    </div>
</template>

<script lang="ts">
    import { Component, Prop, Vue } from 'vue-property-decorator';

    @Component({
        name: 'AppHeader',
    })
    export default class AppHeader extends Vue {
        @Prop(Object) public count!: {};
    }
</script>

<style>

    .app-header {
        align-items: flex-end;
    }

    .app-header h1 {
        flex-grow: 1;
    }

    .app-header h2 {
        font-size: 1.2rem;
        color: grey;
    }

</style>
