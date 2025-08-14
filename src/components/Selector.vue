<template>
    <ul>
        <li @click="setCrypto('BTC')" :class="cryptoNow == 'BTC' ? 'active' : ''">Bitcoin</li>
        <li @click="setCrypto('ETH')" :class="cryptoNow == 'ETH' ? 'active' : ''">ETH</li>
        <li @click="setCrypto('USDT')" :class="cryptoNow == 'USDT' ? 'active' : ''">USDT</li>
    </ul>
    
</template>



<script>
export default {
    props: {
        setCrypto: {
            type: Function,
            required: true
        },
        cryptoNow: {
            type: String,
            required: true
        }
    }
}

</script>



<style scoped>
ul {
    list-style: none;
    max-width: 200px;
    width: 30%;
    border-radius: 3px;
    border: 3px solid #000;
    padding: 0;
}
li {
    background: #1a032d;
    color: #fff;
    padding: 20px;
}
li:hover, li:active {
    background: #2b054a;
    cursor: pointer;
}

.active {
    background: #2b054a;
}



</style>
