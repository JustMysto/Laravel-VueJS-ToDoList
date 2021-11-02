<template>
    <div>
        <div v-for="(item, index) in items" :key="index">
            <list-item
                :item="item"
                class="item"
                v-on:itemChanged="$emit('reloadList')"
            />
        </div>
    </div>
</template>

<script>

import ListItem from './ListItem.vue'

export default {
    props: ['items'],
    components: {
        ListItem
    }
}
</script>

<style lang="scss" scoped>

    .item {
        background-color: #E6E6E6;
        padding: 5px;
        margin-top: 5px;
    }
</style>