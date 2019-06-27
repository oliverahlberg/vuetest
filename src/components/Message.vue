<template>
  <div class="hello">
    <h1
      :class="{ validPassword: validPassword }"
    >
      {{ msg }}
    </h1>
  </div>
</template>

<script>
export default {
  name: 'Clock',
  props: {
    msg: String,
    validPassword: Boolean,
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h1 {
  color: red;
}
.validPassword {
  color: green;
}
</style>
