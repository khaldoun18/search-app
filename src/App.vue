<template >
  <div id="app" class="bg-[#F5F5F5] h-screen p-4">
    <SearchBox />
  </div>
</template>

<script>
import SearchBox from './components/SearchBox.vue';

export default {
  name: 'App',
  components: {
    SearchBox
  }
};
</script>


