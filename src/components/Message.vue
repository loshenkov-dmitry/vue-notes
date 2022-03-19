<template>
  <div class="message">
    <p>{{ message }}</p>
  </div>
</template>

<script>
export default {
  props: {
    message: String,
    required: true,
  },
};
</script>

<style lang="scss" scoped>
.message {
  margin: 20px 0;
  text-align: center;
}
p {
  color: rgb(201, 49, 49);
}
</style>