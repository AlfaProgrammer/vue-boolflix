<template>
    <header>
        <figure class="logo">
            <img :src="netflixLogo" alt="">
        </figure>
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
            netflixLogo: require('../assets/netflix-logo.png')
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
        background-color: #141414;
        margin-bottom: 50px;

        figure{
            img{
                width: 100px;
                object-fit: cover;
                object-position: center;
            }
        }

    }
</style>>

