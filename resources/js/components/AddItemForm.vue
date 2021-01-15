<template>
    <div class="addItem">
        <input
            type="text"
            v-model="item.name"
            @keypress.enter="addItem"
        />
        <font-awesome-icon
            icon="plus-square"
            @click="addItem()"
            :class="[item.name ? 'active' : 'inactive', 'plus']"
        />
    </div>
</template>

<script>
export default {
    data: () => ({
        item: {
            name: ''
        }
    }),
    methods: {
        addItem() {
            if (this.item.name === '') {
                return
            }
            axios.post('api/item/store', {
                item: this.item
            })
            .then(response => {
                if (response.status === 201) {
                    this.item.name = ''
                    this.$emit('reloadlist')
                }
            })
            .catch(error => {
                console.log(error)
            })
        }
    }
}
</script>

<style scoped>
    .addItem{display: flex; justify-content: center; align-items: center;}
    input{background: #f7f7f7; border: 0; outline: 0; padding: 5px; margin-right: 10px; width: 100%;}
    .plus{font-size: 29px;}
    .active{color: #38c172;}
    .inactive{color: #999;}
</style>
