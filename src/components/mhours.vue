<template>
  <div id="map">
    <div class="jianjie" @click="showDialog"><span>简介|功能</span></div>
    <div class="abutton" @click="toggleDdistrict" v-if="districtButton">请选择您所在区域</div>
    <transition name="fade">
    <div class="left-selected" v-if="districtList">
      <div class="left-district-header" ><span @click="isBg" ></span>{{headerName}}</div>
      <div  v-if="isShow"  v-for="item in district" class="left-district" @click="dropNow(item.near,item.name)">{{item.name}}
      </div>
      <transition name="fade">
        <div v-if="isDrop" class="detail-address">
          <ul >
            <li v-for="(local,index) in positions" @click="chooseAddress(index)">{{ local.name}}</li>
            <div v-if="positions==''" style="padding-top: 40px">抱歉(。・＿・。)ﾉ您所在区域没有</div>
          </ul>
        </div>
      </transition>
    </div>
    </transition>
    <!--<div>-->
    <!--<select v-model="selected" class="selected-district">-->
    <!--<option v-for="item in district" :value="item.label" >{{item.name}}</option>-->
    <!--</select>-->
    <!--<div class="selected-detail">-->
    <!--<div class="selection-show" @click="dropNow" ><span>{{ positions[0].name}}</span>-->
    <!--<span class="arrow"></span>-->
    <!--</div>-->
    <!--<div class="selected-list">-->
    <!--<ul v-if="isDrop">-->
    <!--<li v-for="(local,index) in positions" @click="chooseAddress(index)">{{local.name}}</li>-->
    <!--</ul>-->
    <!--</div>-->
    <!--</div>-->
    <!--</div>-->
    <baidu-map :center="center" :zoom="zoom" @ready="handler"  :scroll-wheel-zoom="true" :autoLocation="true" class="bm-view">
      <!--<bm-marker v-for="mark in hoursPoint" :position="{lng:mark.lng,lat:mark.lat}" @click="cl(mark)" :title="mark.name"  animation="BMAP_ANIMATION_BOUNCE">-->
      <!--</bm-marker>-->
      <bm-local-search  :keyword="keyword" :nearby="nearby" :panel="false" :pageCapacity="20"  @searchcomplete="marked" :location="location"></bm-local-search>
    </baidu-map>
    <my-dialog :isLogShow="isShowDialog" @closeDialog="closeDia"></my-dialog>
  </div>
</template>
<script>
  import myDialog from './help'
  export default{
    components:{
      myDialog,
    },
    name: 'mhours',
    data(){
      return{
        isShowDialog:false,
        nearby:{
          center:{
            lng: 116.403981,
            lat:39.915156
          },
          radius:30000,
        },
        districtButton:true,
        districtList:false,
        positions:[],
        location: '北京',
        keyword: '自助图书馆',
        headerName:'请选择您所在区域',
        isShow:true,
        isDrop:false,
        hoursPoint:[ ],
        center: {lng: 0, lat: 0},
        zoom: 12,
        content:'',
        selected:"",
        district:[
          {
            name:"朝阳区",
            label:'chaoyang',
            near:{
              center:{
                lng: 116.534992,
                lat:39.951179
              },
              radius:4000,
            },
          },
          {
            name:"西城",
            label:"xicheng",
            near:{
              center:{
                lng: 116.369974,
                lat:39.924967
              },
              radius:6000,
            },
          },
          {
            name:"东城区",
            value:"dongcheng",
            near:{
              center:{
                lng: 116.424169,
                lat:39.923603
              },
              radius:5800,
            },
          },
          {
            name:"海淀区",
            value:"haidian",
            near:{
              center:{
                lng: 116.250283,
                lat:40.022009
              },
              radius:15300,
            },
          },
          {
            name:"丰台区",
            value:"fengtai",
            near:{
              center:{
                lng: 116.291955,
                lat:39.83516,
              },
              radius:8000,
            },
          },
          {
            name:"大兴区",
            value:"daxing",
            near:{
              center:{
                lng: 116.421365,
                lat:39.65684
              },
              radius:21300,
            },
          },
          {
            name:"石景山区",
            value:"shijingshan",
            near:{
              center:{
                lng: 116.181287,
                lat:39.942861
              },
              radius:8000,
            },
          },
          {
            name:"顺义区",
            value:"shunyi",
            near:{
              center:{
                lng: 116.682263,
                lat:40.16487
              },
              radius:16000,
            },
          },
          {
            name:"通州区",
            value:"tongzhou",
            near:{
              center:{
                lng: 116.767611,
                lat:39.78617,
              },
              radius:20000,
            },
          },
          {
            name:"昌平区",
            value:"changping",
            near:{
              center:{
                lng: 116.239782,
                lat:40.237077
              },
              radius:25000,
            },
          },
          {
            name:"房山区",
            value:"fangshan",
            near:{
              center:{
                lng: 116.03922,
                lat:39.701869
              },
              radius:20000,
            },
          },
        ],
      }
    },
    methods: {
      showDialog(){
        this.isShowDialog=true
      },
      closeDia(){
        this.isShowDialog=false
      },
      toggleDdistrict(){
        this.districtButton=!this.districtButton
        this.districtList=!this.districtList
        this.isDrop=false
        this.isShow=true
      },
      handler ({BMap, map}) {
        console.log(BMap, map)
        this.center.lng = 116.404
        this.center.lat = 39.915
      },
      cl(mark){
        console.log(mark)
        this.zoom=18
        this.center.lng = mark.lng //点击让屏幕移动到点击的标记哪里 center是屏幕
        this.center.lat = mark.lat
        console.log(this.zoom)
      },
      dropNow(ar,an){
        console.log(ar)
//          this.positions=this[ar]//传入的ar为district的label字段“daxing”字段，用this【ar】找到daxing数组，数组传入positions数组
        this.nearby=ar
        console.log(this.nearby)
        this.isDrop=!this.isDrop
        this.isShow=!this.isShow
        this.headerName=an
      },
      chooseAddress(index){
        this.center.lng=this.positions[index].lng
        this.center.lat=this.positions[index].lat
        this.zoom=20
        this.districtButton=!this.districtButton
        this.districtList=!this.districtList
      },
      isBg(){
        if(this.isDrop==false){
          this.districtButton=!this.districtButton
          this.districtList=!this.districtList
        }
        this.isShow=!this.isShow
        this.isDrop=!this.isDrop
        this.headerName="请选择地区"
      },
      marked(results){
        var s = [];
        for (var i = 0; i < results.getCurrentNumPois(); i ++){
//          s.push("{ name" +":"+"'"+ results.getPoi(i).address+"'"+","+"lng"+":"+results.getPoi(i).point.lng+","+"lat"+":"+results.getPoi(i).point.lat+"}");
//        }
          s[i]={name:results.getPoi(i).address,lng:results.getPoi(i).point.lng,lat:results.getPoi(i).point.lat};//直接变成JSON数组
        }
        console.log(s)
        this.positions=s
      }
    },
  }
</script>
<style scoped>
  #map{
    display: flex;
    display: -webkit-flex; /* Safari */
    flex-direction: row-reverse;
    -webkit-flex-direction: row-reverse; /* Safari 6.1+ */
  }
  .bm-view {
    width: 100%;
    height: 812px;
  }
  .abutton{
    position: fixed;
    bottom: 20px;
    width: 200px;
    height: 50px;
    background: white;
    z-index: 3;
    left: 25%;
    line-height: 50px;
    border-radius: 4px;
    -moz-box-shadow:2px 2px 5px #828282;
    -webkit-box-shadow:2px 2px 5px #828282;
    box-shadow:2px 2px 5px #828282;
  }
  .abutton:active{
    background:#efefef ;
  }
  .jianjie{
    position: fixed;
    top: 10px;
    right: 10px;
    width: 100px;
    height: 30px;
    background: #3385ff;
    color: white;
    line-height: 30px;
    border-radius: 9px;
    cursor: pointer;
    z-index: 2;
  }
  .left-selected{
    background: white;
    height: 100%;
    width: 300px;
    z-index: 3;
  }
  .left-district-header{
    border-top: 1px solid 	#efefef;
    width: 300px;
    height: 40px;
    padding: 10px 0;
    border-bottom: 1px solid 	#efefef;
    line-height: 40px;
    font-weight:bold;
  }
  .left-district-header span {
    position: absolute;
    right: 10px;
    cursor: pointer;
    background: url("../assets/back.png")  no-repeat center;
    background-size:contain ;
    width: 40px;
    height: 40px;
    z-index: 99;
  }
  .left-district{
    cursor: pointer;
    width: 100%;
    height: 40px;
    padding: 10px 0;
    border-bottom: 1px solid 	#efefef;
    line-height: 40px;
  }
  .left-district:hover{
    background:#efefef ;
  }
  .detail-address{
    position: fixed;
    right: 0;
    background: white;
    height: 100%;
    width: 300px;
    overflow: scroll;
  }
  .detail-address li{
    cursor: pointer;
    width: 300px;
    height: auto;
    padding: 10px 15px;
    border-bottom: 1px solid 	#efefef;
    line-height: 40px;
    box-sizing:border-box
  }
  .dfade-enter-active{
    transition: all .3s;
  }
  .fade-enter-active{
    transition: all .3s;
  }
  .fade-enter{
    transform: translateX(200px);
  }
</style>

