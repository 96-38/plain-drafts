<template>
  <li class="list-item" v-on:click="remove()">item:{{ contents }}</li>
</template>
<script>
export default {
  props: ["contents", "remove"],
};
</script>
<style scoped></style>
