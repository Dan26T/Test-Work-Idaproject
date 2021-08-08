<template>
    <ul class="items">
        <Item
                v-for="item in items"
                :key="items.id"
                v-bind:item="item"
                v-on:delete-item="deleteItem"
        />
    </ul>
</template>

<script>
    import Item from "@/components/Item";

    export default {
        props: ['items'],
        name: "ItemList",
        components: {
            Item
        },
        methods: {
            deleteItem(id) {
                this.$emit('delete-item', id)
            }
        }
    }
</script>

<style scoped>
    ul {
        list-style: none;
        margin-block-start: 0;
        margin-block-end: 0;

    }

    .items {
        display: grid;
        width: 100%;
        grid-template-columns: 1fr 1fr 1fr;
        grid-gap: 16px;
        padding-inline-start: 0px;
        margin-left: 16px;
        margin-rigth: 16px;
    }

    @media (max-width: 1480px) {
        .items {
            grid-template-columns: 1fr 1fr;
            margin-left: 0;
            margin-right: 0;
            align-items: center;
        }
    }

    @media (max-width: 1023px) {
        .items {
            grid-template-columns: 1fr;
            margin-left: 0;
            margin-right: 0;
        }


    }

    @media (max-width: 767px) {
        .items {
            grid-template-columns: 1fr;
            align-items: center;
            grid-column-gap: 0;
            grid-row-gap: 20px;
        }
    }
</style>