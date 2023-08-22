<template>
  <div>
    This is country page
    {{ coutryDetail[0].name.common }}
    {{ coutryDetail[0].borders }}
    <ul>
      <li
        v-for="country in bordersDetail"
        :key="country.cca3"
        class="hover:shadow-xl"
      >
        <NuxtLink
          :to="{
            name: 'country-name',
            params: {
              name: country.name.common.replaceAll(' ', '-'),
            },
            query: {
              name: country.name.common.replaceAll(' ', '-'),
            },
          }"
          class="block"
        >
          <img class="flag" :src="country.flags.png" :alt="country.flags.alt" />
          {{ country.name.common }}
        </NuxtLink>
      </li>
    </ul>
  </div>
</template>
<script setup>
const route = useRoute();
const bordersString = ref("");
const paramName = route.params.name.replaceAll("-", " ");
// console.log(paramName);
// const name = route.query.name.replaceAll("-", " ");
const { data: coutryDetail } = await useFetch(
  `https://restcountries.com/v3.1/name/${paramName}`
);

coutryDetail.value[0].borders.forEach((item) => {
  bordersString.value = bordersString.value + item + ",";
});
const { data: bordersDetail } = await useFetch(
  `https://restcountries.com/v3.1/alpha?codes=${bordersString.value}`
);
// console.log(bordersDetail.value);
</script>
<style lang="postcss" scoped>
ul {
  @apply list-none flex w-4/5 mx-auto p-0 flex-wrap;

  & li {
    @apply basis-1/4 w-1/4 p-4 rounded-lg;
  }
}

.flag {
  @apply block w-full h-auto;
}
</style>
