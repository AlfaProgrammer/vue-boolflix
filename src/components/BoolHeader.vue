<template>
    <header>
        <div class="logo">Qui logo</div>
        <input type="search" v-model="filter" placeholder="inser text" @keyup.enter="changheFilter">
    </header>
</template>

<script> 

export default {
    name: 'BoolHeader',
    emits:['filterChanged'],
    data(){
        return {
            filter: '',
        }
    },
    methods:{
        changheFilter(){
            this.$emit('filterChanged', this.filter)
        }
    }
}
</script>

<style lang="scss" scoped>
    header{
        display: flex;
        align-items: center;
        justify-content: space-between;
        padding: 10px 20px;
        background-color: salmon;
        margin-bottom: 50px;
    }
</style>>

