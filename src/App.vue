<template>
  <div id="app">
    <test />
  </div>
</template>
<script>
import test from '@/components/test.vue';
export default {
  name: "app",
  components: {
    test
  }
};
</script>
<style>
* {
  font-family: Helvetica;
}

body {
  background-color: #002c6b;
}

::-webkit-scrollbar {
  display: none;
}
</style>
