<template>
    <select v-model="selectFilter" @change="$emit('chane-select', selectFilter )">
        <option v-for="(filter, index) in filters"
                :value="filter.value"
                :key="index"
        >{{filter.label}}
        </option>
    </select>
</template>

<script>
    export default {
        name: "Select",
        data() {
            return {
                selectFilter: 'forName',
                filters: [
                    {label: 'По наименованию', value: 'forName'},
                    {label: 'По цене min', value: 'forPriceMin'},
                    {label: 'По цене max', value: 'forPriceMax'}
                ]
            }
        },
    }
</script>

<style lang="scss" scoped>
    select{
        background: #FFFEFB;
        box-shadow: 0px 2px 5px rgba(0, 0, 0, 0.1);
        border-radius: 4px;
        border:0;
    }
</style>