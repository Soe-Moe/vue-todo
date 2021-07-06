<template>
    <div class="tw-pl-3">
        <ul>
            <li v-for="item in listItems" :key="item.id">
                <div class="tw-relative">
                    <input type="checkbox" :id="'check'+item.id" :checked="item.finished" @change="updateStatus(item.id)"> 
                    <label :for="'check'+item.id" class="tw-ml-2">
                        <del v-if="item.finished" v-text="item.description"></del>
                        <span v-else v-text="item.description"></span>
                    </label>
                    <span class="tw-absolute tw-right-3 tw-cursor-pointer hover:tw-text-red-500" @click="deleteItem(item.id)">Delete</span>
                </div>
            </li>
        </ul>
    </div>
</template>
<script>
export default {
    props: {
        listItems: {
            required: true,
            type: Array
        }
    },
    methods: {
        updateStatus(id){
            let parentData = this.$parent.$data.items;
            let index = parentData.findIndex((item) => item.id == id);
            parentData[index].finished = !parentData[index].finished;
            this.updateLocalStroage(parentData)
        },
        deleteItem(id){
            let parentData = this.$parent.$data.items;
            let index = parentData.findIndex((item) => item.id == id);
            this.$delete(parentData, index);
            this.updateLocalStroage(parentData);
        },
        updateLocalStroage(data){
            localStorage.setItem('todo_items', JSON.stringify(data))
        }
    }
}
</script>