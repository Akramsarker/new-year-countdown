<template>
  <div class="loading">
    <img src="@/assets/loading.gif" alt="loading img" />
  </div>
</template>

<script>
export default {
  data() {
    return {
    };
  },
};
</script>

<style scoped>
.loading {
  display: flex;
  justify-content: center;
  align-items: center;
  width: 100%;
  height: 100vh;
  background: rgb(14, 1, 1);
}
</style>
