<template>

  <HomeModuleTop   @addDayBtn="addDayBtn" v-if="homeShow" @menulineClick="menulineClick" @TileBut="TileBut"></HomeModuleTop>
  <HomeModuleContent  v-if="homeShow" :eventHome="eventApp" :TileButVar="TileButVar" 
  :touchEmit="touchEmit" @delList="delList"></HomeModuleContent>
  <add-day v-if="addDayShow" @returnHome="returnHome" @subDay="subDayApp" :BookKind="BookKind"></add-day>
  <GuanLiBook v-show="addKind" @returnHome="returnHome" @UpBook="UpBook"></GuanLiBook>
  <MyInfo v-if="myInfoShow"></MyInfo>
  <bottom-vue  @guanliClick="guanliClick" @dayClikc="dayClikc" @MyClikc="MyClikc"
  :homeShow="homeShow"></bottom-vue>
  <home-opacity v-if="isHomeOpacity"></home-opacity>
  <side-bar v-if="SideBarShow" :BookKind2="BookKind" :close="closeSidebar" :allAmount="allAmount" :lifeAmount="lifeAmount" :workAmount="workAmount" :memorialDayAmount="memorialDayAmount"></side-bar>
  <!-- <bottom-vue></bottom-vue> -->
</template>

<script>
import HomeModuleTop from './components/HomeModuleTop.vue'
import HomeModuleContent from './components/HomeModuleContent.vue'
import BottomVue from './components/BottomVue.vue'
import AddDay from './components/AddDay.vue'
import GuanLiBook from './components/GuanLiBook.vue'
import MyInfo from './components/MyInfo.vue'
import SideBar from './components/SideBar.vue'
import HomeOpacity from './components/HomeOpacity.vue'


// import BottomVue from './components/BottomVue.vue'
// import HomeModuleBottom from './components/HomeModuleBottom.vue'


export default {
  name: 'App',
  components: {
    HomeModuleTop,
    HomeModuleContent,
    AddDay,
    GuanLiBook,
    BottomVue,
    MyInfo,
    SideBar,
    HomeOpacity,
},
  data(){
    return{
            addDayShow:'',
            homeShow:true,
            eventApp:[],
            addKind:'',
            BookKind:[],
            myInfoShow:'',
            SideBarShow:'',
            // BottomShow:true
            isHomeOpacity:false,
            allAmount:0,
            lifeAmount:0,
            workAmount:0,
            memorialDayAmount:0,
            TileButVar:true,


            //??????????????????????????????
            touchEmit:false,

            //??????????????????id
            nextId:0,
            
            //???????????????id???????????????
            eventparam:{}
    }
  },
  methods:{
    addDayBtn(){
      console.log('??????APPmodule???');
      this.addDayShow=true
      this.homeShow=false
      this.addKind=false
      this.myInfoShow=false
      this.SideBarShow=false
    },
    returnHome(){
      console.log('returnHome?????????')
      this.addDayShow=false
      this.homeShow=true
      this.addKind=false
      this.myInfoShow=false
      this.SideBarShow=false
    },
    test(){
      console.log('test IF ????????????????????????')
    },
    subDayApp(param){
      console.log('submitDay?????????')
      //????????????????????????id
      this.eventparam=param;
      this.nextId++;
      this.eventparam.id=this.nextId;
      console.log('???????????????????????????id???'+this.eventparam.id)

      // const currentEventList = this.eventApp;
      // currentEventList.push(param);
      // this.eventApp= currentEventList;
      if(param.overHeadVar===true){
        const currentEventList = this.eventApp;
        currentEventList.unshift(this.eventparam);
        // currentEventList.unshift(param);
        this.eventApp= currentEventList;
      }
      if(param.overHeadVar===false){
        const currentEventList = this.eventApp;
        currentEventList.push(this.eventparam);
        // currentEventList.push(param);
        this.eventApp= currentEventList;
      }
      console.log('?????????????????????'+this.eventApp)
      // this.eventApp.push(param)
      console.log('App???event:'+this.eventApp)
      console.log('App???event???name:'+this.eventApp.name)
      this.allAmount++;
      if(this.allAmount>=5){
        this.test()
        this.touchEmit=true;
      }
      console.log('?????????????????????'+this.allAmount)
      if(param.kindVar==='??????'){
        this.lifeAmount++;
        console.log('???????????????'+this.lifeAmount)
      }
      if(param.kindVar==='??????'){
        this.workAmount++;
        console.log('???????????????'+this.workAmount)
      }
      if(param.kindVar==='?????????'){
        this.memorialDayAmount++;
        console.log('????????????'+this.memorialDayAmount)
      }
    },
    delList(param6,param7){
      console.log('App????????????????????????')
      this.eventApp.splice(param6,1)
      console.log("??????????????????" + param6, "?????????" + param7);
      
    },
    guanliClick(){
      this.addKind=true;
      this.homeShow=false;
      this.addDayShow=false;
      this.myInfoShow=false
      this.SideBarShow=false
    },
    UpBook(param4){
      this.BookKind=param4;
      console.log('Book????????????'+this.BookKind)
    },
    dayClikc(){
      this.addKind=false;
      this.homeShow=true;
      this.addDayShow=false;
      this.myInfoShow=false
      this.SideBarShow=false
    },
    MyClikc(){
      this.addKind=false;
      this.homeShow=false;
      this.addDayShow=false;
      this.myInfoShow=true;
      this.SideBarShow=false
    },
    menulineClick(){
      this.addKind=false;
      this.homeShow=true;
      this.addDayShow=false;
      this.myInfoShow=false
      this.SideBarShow=true
      // this.BottomShow=false
      this.isHomeOpacity=true;
    },
    closeSidebar(){
      this.SideBarShow = false;
      this.addKind=false;
      this.homeShow=true;
      this.addDayShow=false;
      this.myInfoShow=false
      this.isHomeOpacity=false;
    },
    TileBut(){
      this.TileButVar=!this.TileButVar;
    },
  }
}
</script>

<style>
#app {
  /* font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50; */
  /* margin-top: 60px; */
  font-size: 14px;
}
body{
  background-color: rgb(131, 222, 225);
  margin: 0;
  padding: 0;
}
/* .HomeOpacity{
  width: 100vw;
  height: 109vh;
  background-color: black;
  opacity: 0.4;
  position: absolute;
  z-index: 1;
  position: absolute;
} */
</style>
