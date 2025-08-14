<template>
    <h2>Favoritos</h2>
    <div @click="getFromFavourites(index)" v-for="(element, index) in favourites" :key="index">
        <span>{{ element.from }}</span>
        <span>{{ element.to }}</span>
    </div>
    
</template>



<script>

export default {
    props: {
        favourites: {
            type: Array,
            required: true
        },
        getFromFavourites: {
            type: Function,
            required: true
        }
    }    
}


</script>



<style scoped>

h2 {
    color: #fff;
}

div {
    display: flex;
    justify-content: space-between;
    max-width: 500px;
    width: 40%;
    margin: 0 auto;
    transition: all 500ms ease;
    padding: 5px;
    border: 3px double #8c00ff;
}

span {
    padding: 10px 15px;
    background: #8c00ff;
    color: #fff;
}

div:hover {
    cursor: pointer;
    opacity: 0.7;
    transform: scale(1.1);
}

</style>
