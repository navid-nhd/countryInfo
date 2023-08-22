<template>
  <main>
    <ul>
      <li
        v-for="country in countries"
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
          <img class="flag" :src="country.flags.png" :alt="country.flags.alt" />
          {{ country.name.common }}
        </NuxtLink>
      </li>
    </ul>
  </main>
</template>
<script setup>
const { data: countries } = await useFetch(
  "https://restcountries.com/v3.1/all"
);
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
