<template>
  <div class="home">
    Home page
    <router-link to="/njkt">农技课堂</router-link>
  </div>
</template>
<script>

export default {
  methods: {
    innerJump() {
      this.$router.push('/njkt')
    },
  }
}
</script>