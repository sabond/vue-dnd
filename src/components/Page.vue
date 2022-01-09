<template>
  <div class="page" :data-page-number="pageNumber">Page {{ pageNumber }}</div>
</template>

<script>
export default {
  props: ["pageNumber"]
};
</script>

<style>
.page {
  display: flex;
  flex-direction: column;
  justify-content: center;
  border: solid 1px red;
  height: 200px;
}
</style>
