<template>
  <div class="post-title">
    <h1 v-if="level === '1'">
      <slot />
    </h1>
    <h4 v-if="level === '4'">
      <slot />
    </h4>
  </div>
</template>

<script>
export default {
  props: {
    level: {
      default: '1',
      type: String
    }
  }
}
</script>

<style lang="scss" scoped>
.post-title {
  margin: 20px 0;
  h1,
  h4 {
    background: $primary;
    display: inline;
    color: #fff;
    padding: 5px 20px 5px 10px;
    box-shadow: -10px -10px 0 0 white, 0px 0px 0 0 $primary;
  }
  h4 {
    box-shadow: -5px -5px 0 0 white, 0px 0px 0 0 $primary;
  }
}
</style>
