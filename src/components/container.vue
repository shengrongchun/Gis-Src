<template>
  <div class="container">
    <GisMap ref="Gis"/>
    <div class="menu">
      <a-upload :showUploadList="false" :customRequest="()=>{}" action="" :before-upload="beforeUpload">
        <a-button type="primary" size="small">
          <upload-outlined></upload-outlined>
          上传文件
        </a-button>
      </a-upload>
    </div>
  </div>
</template>
<script>
import GisMap from './gis.vue'
import { ref } from 'vue'
import { UploadOutlined } from '@ant-design/icons-vue'
import { message } from 'ant-design-vue'
const Shapefile = require('shapefile')
export default {
  name: 'gis-container',
  components: {
    GisMap,
    UploadOutlined
  },
  setup() {
    let fileReader = new FileReader()
    const Gis = ref(null)
    //
    const beforeUpload = (file)=> {
      const { name } = file
      if(/.shp$/.test(name)) {
        fileReader.readAsArrayBuffer(file)
        fileReader.onload = function() {
          Shapefile.read(this.result).then((geoJson)=> {
            console.log('geoJson', geoJson)
            Gis.value.drawGeoJSON(geoJson)
          })
        }
        //
        return true
      }
      message.error('请上传.shp文件！')
    }
    return {
      beforeUpload,
      Gis
    }
  }
}
</script>
<style scoped lang="less">
.container {
  height: 100%;
  .menu {
    text-align: center;
    position: fixed;
    top: 0;
    left: 0;
    background: #fff;
    opacity: 0.8;
    height: 100%;
    width: 240px;
    box-shadow: 2px 0 6px 0 rgb(28 32 40 / 30%);
    padding: 20px 10px;
  }
}
</style>