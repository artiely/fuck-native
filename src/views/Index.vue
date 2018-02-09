<template>
  <div class="index">
    <mt-header fixed title="fwone"></mt-header>
    <div class="page-content">
      <div class="fwone-item" @click="toOrder">
        工单处理
      </div>
    </div>
  </div>
</template>

<script>
/*  global plus:true  */
export default {
  name: 'index',
  data() {
    return {
      addresses: '定位中...'
    }
  },
  methods: {
    toDetail() {
      this.$router.push('/detail')
    },
    test() {
      alert(plus.device.imei)
    },
    toOrder() {
      this.$router.push({ name: 'Detail' })
    }
  }
}
</script>
<style>
.fwone-item {
  width: 95%;
  margin: 4px auto;
  padding: 8px;
  box-sizing: border-box;
  box-shadow: 1px 3px 4px rgba(0, 0, 0, 0.2);
  border-radius: 4px;
  min-height: 60px;
  background: #fff;
}
#footer {
  background: #ffffff;
  height: 64px;
  width: 100%;
  padding: 12px;
  position: fixed;
  z-index: 10;
  left: 0px;
  bottom: 0px;
  line-height: 30px;
}
#goto {
  width: 58px;
  height: 58px;
  background: url(../assets/logo.png) no-repeat center center #51c332;
  background-size: 80% 80%;
  position: fixed;
  z-index: 11;
  right: 15px;
  bottom: 15px;
  border-radius: 58px;
}
</style>
