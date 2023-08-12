<template>
  <div class="m-8 p-4">
    <h1 class="text-xl font-bold text-center">Country List</h1>
  </div>
  <CountryList />
</template>

<script>
import CountryList from './components/CountryList.vue'

export default {
  name: 'App',
  components: {
    CountryList
  }
}
</script>
