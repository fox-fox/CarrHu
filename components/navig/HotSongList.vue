<template lang="">
    <div class="top">
        <div class="hotop">
            <div class="hotopct">
                <div class="u-hmsprt hoticon"></div>
                <div class="font_ho">云音乐用户一周内收听所有线上歌曲</div>
                <div class="font_ho">官方TOP排行榜，每周四更新</div>
            </div>
        </div>
        <div class="hotcont">
            <ul class="m-sglst">
                <li v-for="(item, index) in pro" :key="index">
                    <nuxt-link :to="{name:'Player-Details',params:{list_url:item.url,list_pic:item.pic}}">
                        <div class="sgfl sgfl-cred">{{index+1}}</div>
                        <div class="sgfr f-bd f-bd-btm">
                            <div class="sgchfl">
                                <div class="f-thide sgtl">{{item.name}}</div>
                                <div class="f-thide sginfo">{{item.singer}}</div>
                            </div>
                            <div class="sgchfr">
                                <span class="u-hmsprt sgchply"></span>
                            </div>
                        </div>
                    </nuxt-link>    
                </li>
            </ul>
        </div>
    </div>
</template>

<script>
export default {
    data(){
        return{
            pro:[{
                lrc:'',
                singer:'',
                tag:'',
                name:''
            }]
        }
    },
    methods:{
        play_search_content:function(){
            var _this = this;
            _this.$axios
                .get(
                "https://api.itooi.cn/music/netease/songList?key=579621905&id=3778678&limit=10&offset=0"
                )
                .then(function(response) {
                    _this.pro = response.data.data.songs
                    console.log(response.data.data.songs)
                }).catch(function(error) {
                    console.log(error);
                });
        }
    },
    mounted(){
        this.play_search_content();
    }
}
</script>

<style scoped>
.font_ho{color:#fff;text-align:left;margin-top: 8px;}
.recom_tit{margin-bottom: 18px;font-size: 16px;line-height: 20px;text-align: left;padding-left: 10px;color: #333;border-left: 2px solid #d63030}
.Recommend{height: 100%;width: 100%;}
.hotop{position:relative;padding-top:38.9%;overflow:hidden;background:url(/_nuxt/assets/img/bg01.jpg) no-repeat;}
.hotopct{display:-webkit-box;display:-webkit-flex;display:flex;-webkit-box-orient:vertical;-webkit-box-direction:normal;-webkit-flex-direction:column;flex-direction:column;-webkit-box-pack:center;-webkit-justify-content:center;justify-content:center;z-index:2;padding-left:20px;box-sizing:border-box}
.u-hmsprt{background:url(//s3.music.126.net/m/s/img/index_icon_2x.png?5207a28…) no-repeat;background-size:166px 97px}
.hoticon{width:142px;height:67px;background-position:-24px -30px}
.hotop:after,.hotopct{position:absolute;left:0;top:0;right:0;bottom:0}
.top{margin-top:-14px;}
.hotcont{position: relative;}
.sgfl{-webkit-box-align:center;-webkit-align-items:center;align-items:center;width:28px;font-size:17px;color:#df3436;}
.sgfr{display:-webkit-box;display:-webkit-flex;display:flex;position:relative}
.sgchfl,.sgfr{-webkit-box-flex:1;-webkit-flex:1 1 auto;flex:1 1 auto}
.sgchfl,.sgfr{-webkit-box-flex:1;-webkit-flex:1 1 auto;flex:1 1 auto}
.sgchfl{padding:6px 0;width:0;text-align:left;}
.f-thide{overflow:hidden;text-overflow:ellipsis;white-space:nowrap;word-break:normal}
.sgtl{font-size:17px}
.sginfo{font-size:12px;color:#888;padding: 3px 0;}
.sgchfr{display:-webkit-box;display:-webkit-flex;display:flex;-webkit-box-align:center;-webkit-align-items:center;align-items:center;padding:0 10px}
.sgchply{display:inline-block;width:22px;height:22px;background-position:-24px 0}
.f-bd:after{position:absolute;z-index:2;content:"";top:0;left:0;pointer-events:none;box-sizing:border-box;width:100%;height:100%;-webkit-transform-origin:top left;transform-origin:top left;border:0 solid rgba(0,0,0,.1)}
.f-bd:after{width:200%;height:200%;-webkit-transform:scale(.5);transform:scale(.5)}
.f-bd-btm:after{border-bottom-width:1px}
.m-sglst li{padding-left:10px}
.m-sglst li, .sgfl {display: -webkit-box;display: -webkit-flex;display: flex;}
.m-sglst li a{display:flex;width:100%}
</style>