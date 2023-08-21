<template>
    <div>
        hello
        {{ route.params.name }}
    </div>
</template>
<script setup>
const route = useRoute()
console.log(route)
</script>