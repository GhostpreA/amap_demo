<template>
  <div id="container"></div>
</template>

<script>
import AMapLoader from '@amap/amap-jsapi-loader';
import { shallowRef } from '@vue/reactivity'
export default {
  name: 'MapContainer',
  setup(){
    const map = shallowRef(null);
    return{
      map,
    }
  },
  methods:{
    initMap(){
      var that = this;
      AMapLoader.load({
        key:"738506afec3b63bf7c978eb468906f10",             // 申请好的Web端开发者Key，首次调用 load 时必填
        version:"2.0",      // 指定要加载的 JSAPI 的版本，缺省时默认为 1.4.15
        plugins:['AMap.Geolocation','AMap.ToolBar','AMap.Driving'],       // 需要使用的的插件列表，如比例尺'AMap.Scale'等
      }).then((AMap)=>{
        this.map = new AMap.Map("container",{  //设置地图容器id
          viewMode:"3D",    //是否为3D地图模式
          zoom:5,           //初始化地图级别
          center:[105.602725,37.076636], //初始化地图中心点位置

        });
        AMap.plugin(['AMap.Geolocation','AMap.ToolBar','AMap.Driving'], function() {
          var geolocation = new AMap.Geolocation({
            enableHighAccuracy: true,//是否使用高精度定位，默认:true
            timeout: 10000,          //超过10秒后停止定位，默认：无穷大
            maximumAge: 0,           //定位结果缓存0毫秒，默认：0
            convert: true,           //自动偏移坐标，偏移后的坐标为高德坐标，默认：true
            showButton: true,        //显示定位按钮，默认：true
            buttonPosition: 'LB',    //定位按钮停靠位置，默认：'LB'，左下角
            buttonOffset: new AMap.Pixel(10, 20),//定位按钮与设置的停靠位置的偏移量，默认：Pixel(10, 20)
            showMarker: true,        //定位成功后在定位到的位置显示点标记，默认：true
            showCircle: true,        //定位成功后用圆圈表示定位精度范围，默认：true
            panToLocation: true,     //定位成功后将定位到的位置作为地图中心点，默认：true
            zoomToAccuracy:true      //定位成功后调整地图视野范围使定位位置及精度范围视野内可见，默认：false
          });
          var toolbar = new AMap.ToolBar();
          that.map.addControl(toolbar);
          var driving = new AMap.Driving();//驾车路线规划
          driving.search(/*参数*/)

          geolocation.getCurrentPosition(function(status,result){
            if(status=='complete'){
              onComplete(result)
            }else{
              onError(result)
            }
          });

          function onComplete (data) {
            // data是具体的定位信息
          }

          function onError (data) {
            // 定位出错
          }
          // geolocation.getCurrentPosition();
          // AMap.event.addListener(geolocation, 'complete', onComplete);//返回定位信息
          // AMap.event.addListener(geolocation, 'error', onError);      //返回定位出错信息
        })

      }).catch(e=>{
        console.log(e);
      })
    },
  },
  mounted(){
    //DOM初始化完成进行地图初始化
    this.initMap();

  }

}


</script>

<style scoped>
  #container{
    padding:0px;
    margin: 0px;
    width: 100%;
    height: 800px;
  }
</style>
