<template>
  <div class="hello">
    <router-link tag="p" to="/movies">{{ msg }}</router-link>
    <router-link tag="p" to="/me">当前有{{ userCount.length }}条收藏记录 >></router-link>
  </div>
</template>

<script>

export default {
  data () {
    return {
      msg: '主页空空如也:) 去看看电影吧 >>'
    }
  },
  computed: {
    userCount() {
      return this.$store.getters.getLocalData
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
  p {
    padding: 2px 5px;
    color: darkslategray;
  }
</style>
