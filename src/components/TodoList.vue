<template>
    <div class="tw-flex tw-items-center">
        <div class="tw-w-96 tw-mt-10 tw-mx-auto tw-bg-white tw-rounded-lg tw-p-3">
            <h2 class="tw-text-lg tw-font-bold tw-pb-2 tw-mb-3 tw-text-center tw-border-0 tw-border-b tw-border-solid tw-border-gray-200">Todo List</h2>
            <list-items :list-items="items" v-if="items.length > 0"></list-items>
            <p v-else class="tw-text-center">No list item</p>
            <todo-input></todo-input>
        </div>
    </div>
</template>
<script>
import ListItems from './ListItems'
import TodoInput from './TodoInput'

export default {
    components:{
        ListItems,
        TodoInput
    },
    data: () => {
        return {
            items: [
                
            ]
        }
    },
    mounted(){
        this.loadFromStroage()
    },
    methods: {
        loadFromStroage(){
            const data = JSON.parse(localStorage.getItem('todo_items'))
            this.items = data ? data : []
        }
    }
}
</script>