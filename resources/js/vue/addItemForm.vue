<template>
    <div class="addItem">
        <input type="text" v-model="item.name">
        <font-awesome-icon @click="addItem()" :class="[item.name ? 'active' : 'inactive', 'plus']" icon="plus-square" />
    </div>
</template>

<script>
export default {
    data() {
        return {
            item: {
                name: ''
            }
        }
    },
    methods: {
        addItem() {
            if (this.item.name == "") {
                return;
            }
            axios
            .post("api/item/store", {
                    item: this.item,
                })
                .then((response) => {
                    if (response.status == 201) {
                        this.item.name = "";
                        this.$emit('reloadlist');
                    }
                })
                .catch((error) => {
                    console.log(error);
                });
        },
    }
}
</script>

<style scoped>
.addItem {
    display: flex;
    justify-content: center;
    align-items: center;
}

input {
    background: #f7f7f7;
    border: 0;
    outline: none;
    padding: 5px;
    margin-right: 10px;
}

.plus {
    font-size: 20px;
    cursor: pointer;
}

.active {
    color: #00ce25;
}

.inactive {
    color: #999
}
</style>
