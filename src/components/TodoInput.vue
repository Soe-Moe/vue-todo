<template>
    <div class="tw-mt-4 tw-w-full">
        <input type="text" v-model="input" class="tw-w-3/4 tw-px-2 tw-py-1 tw-outline-none tw-border tw-border-solid tw-border-gray-200 tw-border-r-0">
        <button class="tw-w-3/12 tw-border tw-border-solid tw-border-gray-200 tw-py-1 tw-px-3" @click="submit()">Submit</button>
    </div>
</template>
<script>
export default {
    data: () => {
        return {
            id: 0,
            input: ''
        }
    },
    methods: {
        submit(){
            let description = this.input,
                parentData = this.$parent.$data.items;
                this.id = this.id +1

            if(description != ''){
                parentData.push({
                    id : this.id,
                    description,
                    finished: false
                })
            }

            this.updateLocalStorage(parentData)
            
            this.input = ''
        },
        updateLocalStorage(data){
            localStorage.setItem('todo_items', JSON.stringify(data))
        }
    }
}
</script>