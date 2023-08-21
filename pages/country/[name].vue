<template>
    <div>
        This is country page
        {{ coutryDetail[0].name.common}}
        {{ coutryDetail[0].borders }}
    </div>
</template>
<script setup>
const route = useRoute()
const bordersString = ref('')
const name = route.query.name.replaceAll('-', ' ')
const { data : coutryDetail } = await useFetch(`https://restcountries.com/v3.1/name/${name}`)

coutryDetail.value[0].borders.forEach(item => {
    bordersString.value = bordersString.value+item+','
});
const { data : bordersDetail } = await useFetch(`https://restcountries.com/v3.1/alpha?codes=${bordersString.value}`)
console.log(bordersDetail.value)
</script>