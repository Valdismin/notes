<template>
  <div class="message">
    <p>{{ message }}</p>
  </div>
</template>

<script>
export default {
  name: "MessageComponent",
  props: {
    message: {
      type: String,
      default: "Default Message"
    }
  }
}
</script>

<style lang="scss" scoped>
.message {
  color: red;
}
</style>
