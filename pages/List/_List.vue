<template>
    <div class="list">
        <div class="header">
            <div class="heaader_bg" :style="{backgroundImage: 'url(' + Song.songListPic + ')'}"></div>
            <div class="plhead_wrap">
                <div class="plhead_fl lsthd_fl">
                    <img class="u-img" :src="Song.songListPic">
                </div>
                <div class="plhead_fr">
                    <h2 class="lsthd_title">{{Song.songListName}}</h2>
                </div>
            </div>
        </div>
        <div class="pylst_intro">
            <div class="lstit_tags">
                标签：
                <!-- <em class="f-bd f-bd-full lstit_tag" v-for="(item,index) in items" v-bind:key="index">
                    
                </em> -->
            </div> 
            <div class="u-intro">
                <p class="list_i">简介: &nbsp;  {{Song.songListDescription}}</p>
            </div>      
        </div>
        
        
        <div class="pylst_list">
            <h3 class="u-smtitle">歌曲列表</h3>
            <ol class="u-songs">
                <li class="u-song" v-for="(item,index) in songs" v-bind:key="index">
                    <nuxt-link :to="{name:'Player-Details',params:{list_url:item.url,list_pic:item.pic}}">
                        <div class="sgi_fl">{{index+1}}</div>
                        <div class="sgi_fr f-bd f-bd-btm">
                            <div class="sgich_fl">
                                <div class="f-thide sgich_tl">{{item.name}}</div>
                                <div class="f-thide sgich_info">{{item.singer}}</div>
                            </div>
                            <div class="sgich_fr">
                                <span class="u-hmsprt sgich_ply"></span>
                            </div>
                        </div>
                    </nuxt-link>
                </li>
            </ol>
        </div>
    </div>
</template>

<script>
import indexCss from '~/assets/index.css'

var songs=[];
export default {
    components:{
       
    },
    data(){
        return{
            ID:this.$route.params.List,
            Song:[{
                songListPic:'',
                songListDescription:'',
                songListName:''
            }],
            songs:[{
                name:'',
                pic:'',
                singer:'',
                url:''
            }]
        }
    },
    methods:{
        list:function(){
            var _this = this;
            var id = this.ID;
            // console.log(id);
            _this.$axios
                .get(
                "https://api.bzqll.com/music/netease/songList?key=579621905&id="+id+"&limit=10&offset=0"
                )
                .then(function(response) {
                    _this.Song = response.data.data;
                    _this.songs = response.data.data.songs;
                    console.log(_this.songs)
                }).catch(function(error) {
                    console.log(error);
                });
        }
    },
    mounted(){
        this.list()
    }
}
</script>

<style scoped>
.header{position: relative;padding: 30px 10px 30px 15px;overflow: hidden;}
.heaader_bg{position: absolute;left: 0;top: 0;right: 0;bottom: 0;z-index: 1;background-repeat: no-repeat;background-size: cover;background-position: 50%;-webkit-filter: blur(20px);filter: blur(20px);-webkit-transform: scale(1.5);transform: scale(1.5);}
.heaader_bg::after{content: " ";background-color: rgba(0,0,0,.25);}
.plhead_wrap{display: flex;position: relative;z-index: 2;}
.plhead_fl{position: relative;width: 126px;height: 126px;background-color: #e2e2e3;}
.u-img{width: 100%;vertical-align: middle;}
.plhead_fr{-webkit-box-flex: 1;-webkit-flex: 1 1 auto;flex: 1 1 auto;width: 1%;margin-left: 16px;}
.lsthd_title{padding-top: 1px;font-size: 17px;line-height: 1.3;color: #fefefe;height: 44px;display: -webkit-box;-webkit-box-pack: center;overflow: hidden;text-overflow: ellipsis;-webkit-line-clamp: 2;-webkit-box-orient: vertical;}
.pylst_intro {position: relative;margin: 0 10px 0 15px;padding-top: 10px;line-height: 19px;color: #666;}
.lstit_tags{margin-bottom: 10px;line-height: 20px;margin-right: -10px;}
.f-bd{position: relative;border-bottom: 1px solid #eee;}
.lstit_tag{display: inline-block;margin-right: 10px;padding: 1px 8px;font-size: 12px;}
.lstit_tag:after{position: absolute; z-index: 2;content: ""; top: 0;left: 0;pointer-events: none;box-sizing: border-box; width: 100%; height: 100%;-webkit-transform-origin: top left;transform-origin: top left;border: 0 solid rgba(0,0,0,.1);border-radius: 9999px;border-width: 1px;width: 200%;height: 200%;-webkit-transform: scale(.5);transform: scale(.5);}
.u-intro { position: relative;padding-bottom: 18px;line-height: 19px; color: #666;}
.f-brk {word-wrap: break-word;word-break: break-all;white-space: normal;}
.list_i{font-size: 14px;color: #666}

.pylst_list{}
.u-smtitle{height: 23px;line-height: 23px;padding: 0 10px; font-size: 12px;color: #666;background-color: #eeeff0;}
.u-song{display: -webkit-box;display: -webkit-flex;display: flex;}
.u-song .sgi_fl{-webkit-box-align:center;-webkit-align-items:center;align-items:center;-webkit-box-pack:center;-webkit-justify-content:center;justify-content:center;width:40px;font-size:17px;color:#999}
.u-song .sgi_fl,.u-song .sgi_fr{display:-webkit-box;display:-webkit-flex;display:flex}
.u-song .sgi_fl,.u-song .sgi_fr{display:-webkit-box;display:-webkit-flex;display:flex}
.u-song .sgi_fr{position:relative}
.u-song .sgi_fr,.u-song .sgich_fl{-webkit-box-flex:1;-webkit-flex:1 1 auto;flex:1 1 auto}
.u-song .sgich_fl{padding:6px 0;width:0}
.f-thide{overflow:hidden;text-overflow:ellipsis;white-space:nowrap;word-break:normal}
.u-song .sgich_tl{font-size:17px}
.f-thide{overflow:hidden;text-overflow:ellipsis;white-space:nowrap;word-break:normal}
.u-song .sgich_info{font-size:12px;color:#888}
.u-song .sgich_fr{display:-webkit-box;display:-webkit-flex;display:flex;-webkit-box-align:center;-webkit-align-items:center;align-items:center;padding:0 10px}
.u-song .sgich_ply{display:inline-block;width:22px;height:22px;background-position:-24px 0}
.u-hmsprt{background:url(//s3.music.126.net/m/s/img/index_icon_2x.png?5207a28…) no-repeat;background-size:166px 97px}
.f-bd-btm:after{border-bottom-width: 1px;}
.f-bd:after{position:absolute;z-index:2;content:"";top:0;left:0;pointer-events:none;box-sizing:border-box;width:100%;height:100%;-webkit-transform-origin:top left;transform-origin:top left;border:0 solid rgba(0,0,0,.1)}
.f-bd:after{width: 200%;height: 200%;-webkit-transform: scale(.5);transform: scale(.5);}
.u-song a{display: inherit;width: 100%;}





</style>









