<template>
    <div class="content">
        <InfoBox :clickEventlist="ClickEventlist" v-show="TileButVar"></InfoBox>
        <day-list :eventList="eventHome" @ShowInfo="showInfo" 
        :TileButVar="TileButVar" :touchEmit="touchEmit"
        @delList="delList"></day-list>
        <!-- <bottom-vue @guanliClick="guanliClick($emit('guanliClick'))"></bottom-vue> -->
    </div>
</template>

<script>
// import BottomVue from './HomeModuleContent/BottomVue.vue'
import DayList from './HomeModuleContent/DayList.vue'
import InfoBox from './HomeModuleContent/InfoBox.vue'


export default {
  components: { 
    InfoBox,
    DayList,
    // BottomVue ,
}, 
data(){
    return{
        ClickEventlist:{}
    }
}
,
    props:{
        eventHome:Array,
        TileButVar:Boolean,
        touchEmit:Boolean,
    },
    methods:{
        showInfo(param1){
            console.log('list被点击传来的东西:'+param1)
            this.ClickEventlist=param1;
            console.log('ClickEventlist:'+this.ClickEventlist)
            console.log('ClickEventlist的属性:'+this.ClickEventlist.name)
        },
        delList(param3,param5){
            this.$emit('delList',param3,param5)
        }
    }
}
</script>
<style scoped>
.content{
    height:91vh;
    display: flex;
    flex-direction: column;
    /* 水平居中 */
    align-items: center;
    justify-content: space-between;
}
</style>