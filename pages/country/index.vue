<template>
    <div>
        This is country page
        {{ coutryDetail[0].borders }}
    </div>
</template>
<script setup>
const route = useRoute()
const name = route.query.name
const { data : coutryDetail } = await useFetch(`https://restcountries.com/v3.1/name/${name}`)
</script>