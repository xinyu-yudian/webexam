<template>
    <div id="cesiumcss">
    </div>
</template>

<script>


export default {
    name:'MyCesium',
    data(){
      return{
        viewer:null
      }
    },
    methods:{
        FirstCesium(){
            Cesium.Ion.defaultAccessToken = "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJqdGkiOiJhODNmYTAzNi1iODIzLTQyZjMtYTllNS04YmJhODc5ZmZlYzUiLCJpZCI6MTEwMDk5LCJpYXQiOjE2NjQ5MzQ1OTJ9.odYlivwwPYJNnNwfVSBi5Qnfc3G7TAg_6Y1LjlLXBYc",
            this.viewer =  new Cesium.Viewer("cesiumcss")
        }
    },
    mounted(){
        this.FirstCesium();
    }
}
</script>

<style scoped>
  /* #cesiumcss{
    widows: 100%;
    height: 100%;
  } */
</style>
