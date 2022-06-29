<template>
  <div class="bg-gradient-to-r from-cyan-200 to-sky-400 wrapper">
    <Form />
  </div>
</template>

<script>
import Form from "../components/Form.vue";

export default {
  name: "App",
  components: {
    Form,
  },
};
</script>

<style lang="postcss">
#app {
  height: 100vh;
}
.wrapper {
  height: 100%;
  @apply flex items-center justify-center;
}
</style>
