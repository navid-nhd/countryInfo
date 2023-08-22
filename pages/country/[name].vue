<template>
  <div class="container mx-auto pt-9">
    <div class="flex gap-12 mb-8">
      <div class="image p-1 rounded-lg">
        <div class="rounded-lg bg-black p-1">
          <img
            class="w-full rounded-lg"
            :src="coutryDetail[0].flags.png"
            :alt="coutryDetail[0].flags.alt"
          />
        </div>
      </div>
      <div class="details flex flex-col gap-4">
        <div class="name text-2xl font-bold">
          {{ coutryDetail[0].name.common }}
        </div>
        <div class="name text-xl font-bold">
          Capital : {{ coutryDetail[0].capital[0] }}
        </div>
        <div class="text-lg font-medium">
          Population: {{ coutryDetail[0].population.toLocaleString() }}
        </div>
        <div class="flex gap-2">
          Continents:
          <div v-for="(i, index) in coutryDetail[0].continents" :key="index">
            {{ i }}
            <span v-show="coutryDetail[0].continents.length > 1"></span>
          </div>
        </div>
        <div>Time Zone: {{ coutryDetail[0].timezones[0] }}</div>
      </div>
    </div>

    <div class="">
      <h1 class="text-xl font-bold ml-6">neighbor countries:</h1>
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
            }"
            class="block"
          >
            <img
              class="flag"
              :src="country.flags.png"
              :alt="country.flags.alt"
            />
            {{ country.name.common }}
          </NuxtLink>
        </li>
      </ul>
    </div>
  </div>
</template>
<script setup>
useHead({
  bodyAttrs: {
    class: "bg-[#D3D3D3]",
  },
});
const route = useRoute();
const bordersString = ref("");
const paramName = route.params.name.replaceAll("-", " ");

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
