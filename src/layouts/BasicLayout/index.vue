<template>
  <div class="menu">

  </div>
</template>
<script>
export default {
  computed: {
    value () {
      return this.$route.path
    }
  },
  methods: {
    handleSelect (key) {
      this.$router.push(key)
    }
  },
};
</script>

<style lang="css" scoped>
.menu {
  height: 100%;
  width: 200px;
}
</style>
