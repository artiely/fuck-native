<template>
  <div class="index">
    <mt-header fixed title="index"></mt-header>
    <div class="page-content">
      <div id="map" style="width:100%; height:500px;"></div>
      <div id="footer">
        [当前位置]<br />
        <span id="address">{{addresses}}</span>
      </div>
      <div id="goto" @click="goto"></div>
      <mt-button @click="test">获取设备id</mt-button>
    </div>
  </div>
</template>

<script>
/*  global plus:true  */
export default {
  name: 'index',
  data() {
    return {
      addresses:'定位中...'
    }
  },
  methods: {
    toDetail() {
      this.$router.push('/detail')
    },
    test() {
      alert(plus.device.imei)
    },
    goto() {
      // plus.maps.openSysMap(center, address, center)
    }
  },
  created() {
    var map, center, address
    var _this = this
    function showMap() {
      plus.nativeUI.showWaiting()
      // 创建地图
      map = new plus.maps.Map('map')
      // 设置缩放级别
      map.setZoom(18)
      // 开启用户位置显示
      map.showUserLocation(true)
      // 获取用户位置信息
      map.getUserLocation((state, point) => {
        console.log(JSON.stringify(point))
        center = new plus.maps.Point(point.longitude, point.latitude)
        // 设置地图中心点
        map.setCenter(center)
        // 在周围设置图标 "latitude":34.2337,"longitude":108.903271,
        var bike1 = new plus.maps.Point(point.longitude + 0.0001, point.latitude + 0.0003)
        var bike1Icon = new plus.maps.Marker(bike1)
        bike1Icon.setIcon('../assets/logo.png')
        // var bubble = new plus.maps.Bubble("打造最好的HTML5移动开发工具")
        // bike1Icon.setBubble(bubble)
        map.addOverlay(bike1Icon)
        // var bike1 = new plus.maps.Point(point.longitude - 0.0001, point.latitude - 0.0003)
        // var bike1Icon = new plus.maps.Marker(bike1)
        // bike1Icon.setIcon('../assets/logo.png')
        // var bubble = new plus.maps.Bubble("打造最好的HTML5移动开发工具")
        // bike1Icon.setBubble(bubble)
        // map.addOverlay(bike1Icon)
      })
      // 获取用户地址信息
      plus.geolocation.getCurrentPosition((p) => {
        plus.nativeUI.closeWaiting()
        console.log(JSON.stringify(p))
        address = p.address.poiName
        _this.addresses = p.addresses
        console.log(_this.addresses)
      }, () => {
      })
    }
    document.addEventListener('plusready', () => {
      var winHeight = document.documentElement.clientHeight
      document.getElementById('map').style.height = (winHeight - 188) + 'px'
      showMap()
    })
  }
}
</script>
<style>
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
