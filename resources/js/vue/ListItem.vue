<template>
    <div class="item">
        <input type="checkbox"
            @change="updateCheck()"
            v-model="item.completed"
        />
        <span :class="[item.completed ? 'completed' : '', 'item-text']">{{ item.name }}</span>
        <button @click="removeItem" class="trashcan">
            <font-awesome-icon icon="trash" />
        </button>
    </div>
</template>

<script>
export default {
    props: ['item'],
    methods: {
        updateCheck() {
            axios.put('api/item/' + this.item.id, {
                item: this.item
            })
            .then(response => {
                if (response.status == 200) {
                    this.$emit('itemChanged')
                }
            })
            .catch(error => {
                console.log(error)
            })
        },
        removeItem() {
            axios.delete('api/item/' + this.item.id)
            .then(response => {
                if (response.status == 200) {
                    this.$emit('itemChanged')
                }
            })
            .catch(error => {
                console.log(error)
            })
        }
    }
}
</script>

<style lang="scss" scoped>

    .item {
        display: flex;
        justify-content: center;
        align-items: center;

        .item-text {
            width: 100%;
            margin-left: 20px;

            &.completed {
                text-decoration: line-through;
                color: #999999;
            }
        }

        .trashcan {
            background-color: #E6E6E6;
            border: none;
            color: red;
            outline: none;
        }
    }

</style>