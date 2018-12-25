<template>
    <div class="app1">
        <ul class="ul_01">
            <li v-for="(item,index) in items" @click="oitems(index)" v-bind:class="{active : this_index == index }" v-bind:key="item.id">
                <span>{{item}}</span> 
            </li>
        </ul>
        <ul class="ul_02">
            <li v-bind:class='{active : this_index == 0 }'>
                <recommend />
            </li>
            <li v-bind:class='{active : this_index == 1 }'>
                <ReGe />
            </li>
            <li v-bind:class='{active : this_index == 2 }'>
                <sousuo />
            </li>


            <!-- <li v-for="(ul02,b) in ul_data" v-bind:class='{active : this_index == b }' v-bind:key="ul02.id">
            {{ul02}} -->
            
            
        </ul>
        
    </div>  
</template>


<script>
import recommend from '~/components/navig/Recommend.vue'
import ReGe from '~/components/navig/HotSongList.vue'
import sousuo from '~/components/navig/Search.vue'
export default {
    components:{
        recommend,
        ReGe,
        sousuo
    },
    data(){
        return{
            items:['推荐音乐','热歌榜','搜索'],
            this_index:0
        }
    },
    methods:{
        oitems:function(index){
            this.this_index=index;
        }
    }
}
</script>


<style scoped>
.app1{width: 100%;height: 100%;}
.ul_01{width: 100%;height: 40px;background: #fff;border-bottom: 2px solid #eee;padding-bottom: 20px;position: fixed;top:64px;z-index: 10;}
.ul_01 li{width: 30%;float: left;text-align: center;margin-right: 5%;transition: all .3s;}
.ul_01 li span{color:#333;line-height: 40px;font-size: 15px;cursor: pointer;}
.ul_01 li:last-child{margin-right: 0;}
.ul_01 li.active span{color: #d63030;}
.ul_02::after{content: "";display: block;clear: both;}
.ul_02{width: 100%;height: 100%;position: relative;padding-top: 54px;}
.ul_02 li{width: 100%;height: 100%;text-align: center;color: #FFFFFF;transition: all .3s;display: none;}
.ul_02 li.active{display: block} 
</style>




