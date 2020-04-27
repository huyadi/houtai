<template>
  <div>
    <h1>
      <el-button @click="tuichu" type="info" size="mini">退出</el-button>
    </h1>
  </div>
</template>

<script>
export default {
  data() {
    return {}
  },
  created() {},
  mounted() {},
  methods: {
    // 退出
    tuichu() {
      window.sessionStorage.clear()
      this.$router.push('/login')
    }
  }
}
</script>

<style scoped lang="less"></style>
