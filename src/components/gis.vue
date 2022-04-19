<template>
  <div id='gis-container'></div>
</template>
<script>
import AMapLoader from '@amap/amap-jsapi-loader'
import { onMounted } from 'vue'
//
export default {
  name: 'GisMap',
  setup() {
    let map = null
    let AMap = null
    //
    const initMap = ()=> {
      AMapLoader.load({
        key:['84d6aa44c241a991f9c68ab5757a21c2'],  //设置您的key
        version: "2.0",
        plugins:['AMap.ToolBar','AMap.ControlBar','AMap.GeoJSON'],
        AMapUI:{
          version:"1.1",
          plugins:[],
        },
        Loca:{
          version:"2.0.0"
        },
      }).then((aMap) => {
        AMap = aMap
        map = new AMap.Map("gis-container",{
          pitch: 10, // 地图俯仰角度，有效范围 0 度- 83 度
          viewMode: '3D',
          zoom: 18,
          zooms: [2,20],
          center: [118.796623, 32.059352],
        })
        const controlBar = new AMap.ControlBar({
          position:{
            right:'10px',
            top:'10px'
          }
        })
        controlBar.addTo(map)
        const toolBar = new AMap.ToolBar({
          position:{
            right:'40px',
            top:'110px'
          }
        })
        toolBar.addTo(map)
        //
      }).catch(e => {
        console.error(e)
      })
    }
    const drawGeoJSON = (geoJSON)=> {
      const geojson = new AMap.GeoJSON({
        geoJSON,
      })
      map.add(geojson)
    }
    onMounted(()=> {
      initMap()
    })
    return{
      map,
      drawGeoJSON
    }
  }
}
</script>
<style scoped lang="less">
#gis-container {
  padding: 0px;
  margin: 0px;
  width: 100%;
  height: 100%;
}
</style>