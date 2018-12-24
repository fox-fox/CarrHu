<template>
    <div class="Recommend">
        <h2 class="recom_tit">推荐歌单</h2>
        <div class="content">
            <!-- {{pro}} -->
            <ul class="content_ul">
                <li v-for="(item,index) in pro" v-bind:key="index">
                    <nuxt-link :to='"/List/"+item.id'>
                        <img v-bind:src="item.coverImgUrl">
                        <span class="li_tit">{{item.title}}</span>
                    </nuxt-link>
                </li> 
            </ul>
        </div>
    </div>
</template>


<script>
var pro =[];
export default {
    data(){
        return{
            pro:[{
               coverImgUrl:'',
                title:'',
                id:''
            }]
        }
    },
    methods:{
        play_search_content:function(){
            var _this = this;
            _this.$axios
                .get(
                "https://api.bzqll.com/music/netease/hotSongList?key=579621905&cat=全部&limit=10&offset=0"
                )
                .then(function(response) {
                    _this.pro = response.data.data;
                    // console.log(_this.pro)
                }).catch(function(error) {
                    console.log(error);
                });
        }
    },
    mounted(){
        this.play_search_content();
    }
}

// https://api.bzqll.com/music/netease/songList?key=579621905&id=2547789676&limit=10&offset=0 //歌单
</script>

<style scoped>
.recom_tit{margin-bottom: 18px;font-size: 16px;line-height: 20px;text-align: left;padding-left: 10px;color: #333;border-left: 2px solid #d63030}
.Recommend{height: 100%;width: 100%;}
.li_tit{color: #333;text-align: left;display: block;-webkit-box-orient: vertical;padding: 6px 2px 0 6px;font-size: 13px;max-height: 40px;overflow: hidden;}
.content_ul{display: flex;-webkit-box-pack: justify;-webkit-justify-content: space-between;-ms-flex-pack: justify;justify-content: space-between;flex-wrap: wrap;-webkit-wrap: wrap;}
.content_ul li{width: 32%;float: left;line-height: inherit;margin-bottom: 20px;} 
.content_ul li img{max-width: 100%;height:inherit;display: block;margin: 0 auto;}
.content_ul:after{content:"";display:block;clear:both;}
</style>

