<template>
    <input type="number" min="0" @input="changeAmount($event.target.value)" placeholder="Introduce un numero">
</template>



<script>
export default {
    props: {
        changeAmount: {
            type: Function,
            required: true
        }
    }
}

</script>



<style scoped>
input {
    display: block;
    margin: 20px auto;
    border-radius: 5px;
    border: 0;
    padding: 8px;
    width: 80%;
    max-width: 540px;
}
input:focus {
    outline: none;
    box-shadow: none;
}

</style>
