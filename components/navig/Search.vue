<template>
    <div class="m-tabct">
        <div class="tabctitem">
            <div class="m-hmsrch">
                <form class="m-input f-bd f-bd-btm" method="get" action="#">
                    <div class="inputcover">
                        <i class="u-svg u-svg-srch"></i>
                        <input id="" @focus="focus1" @blur="blur1" @input="inputFun" type="search"  class="input" placeholder="" value="" >
                        <label class="holder" v-bind:class="{active : isdisplay == true}" >搜索歌曲、歌手、专辑</label>
                        <div class="close">
                            <i class="u-svg u-svg-empty"></i>
                        </div>
                    </div>
                </form>
                <div class="m-default">
                    <section class="m-hotlist">
                        <h3 class="title">{{ssage}} <a @click="search1">{{emm}}</a></h3>
                        <ul class="list">
                            <li class="item f-bd f-bd-full">
                                <a class="link" href="javascript:void(0);">圣诞</a>
                            </li>
                        </ul>
                         <div class="hotcont">
                            <ul class="m-sglst" :class="{active : isActive == true}">
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
                    </section>
                </div>
            </div>
        </div>
    </div>
</template>


<script>
export default {
    data(){
        return{
            ssage:'热门搜索',
            message:'',
            isdisplay: false,
            isActive:true,
            emm:'',
            pro:[{
                name:'',
                singer:'',
                id:'',
                url:'',
                lrc:''
            }]
        }
    },
    methods:{
        inputFun(e){
            this.ssage = '搜索';
            this.emm = e.target.value;
            if(e.target.value.length > 0){
                this.isdisplay = true;
            }
        },
        focus1(e){
            this.isdisplay = true
        },
        blur1(e){
            if(e.target.value.length <= 0){
                this.isdisplay = false;
                this.ssage ='热门搜索'
            }
        },
        search1(){
            if(this.emm.length > 0){
                var _this = this;
                _this.$axios
                .get(
                "https://api.bzqll.com/music/netease/search?key=579621905&s="+this.emm+"&type=song&limit=100&offset=0"
                )
                .then(function(response) {
                    _this.pro = response.data.data;
                    _this.isActive = false;
                    console.log(_this.pro)
                }).catch(function(error) {
                    console.log(error);
                });
            }
        }
    },
    mounted(){
        
    }
}
</script>


<style scoped>
.m-tabct{margin-top:-14px;}
.m-tabarea .m-tabct{display:block}
.m-tabarea .m-tabct,.m-tabct .tabctitem{width:100%;height:100%}
.m-tabarea .m-tabct,.m-tabct .tabctitem{width:100%;height:100%}
.m-hmsrch{background:#fbfcfd}
.f-bd{position:relative}
.f-bd:after{position:absolute;z-index:2;content:"";top:0;left:0;pointer-events:none;box-sizing:border-box;width:100%;height:100%;-webkit-transform-origin:top left;transform-origin:top left;border:0 solid rgba(0,0,0,.1)}
.m-input{padding:15px 10px}
.m-input .inputcover{position:relative;width:100%;height:30px;padding:0 30px;box-sizing:border-box;background:#ebecec;border-radius:30px}
.u-svg-srch{width:13px;height:13px;background-image:url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHZpZXdCb3g9IjAgMCAyNiAyNiI+PHBhdGggZmlsbC1ydWxlPSJldmVub2RkIiBmaWxsPSIjYzljOWNhIiBkPSJNMjUuMTgxLDIzLjUzNWwtMS40MTQsMS40MTRsLTcuMzE1LTcuMzE0CgkJQzE0LjcwOSwxOS4xMDcsMTIuNDYsMjAsMTAsMjBDNC40NzcsMjAsMCwxNS41MjMsMCwxMEMwLDQuNDc3LDQuNDc3LDAsMTAsMGM1LjUyMywwLDEwLDQuNDc3LDEwLDEwYzAsMi4zNDItMC44MTEsNC40OS0yLjE2LDYuMTk1CgkJTDI1LjE4MSwyMy41MzV6IE0xMCwyYy00LjQxOCwwLTgsMy41ODItOCw4czMuNTgyLDgsOCw4YzQuNDE4LDAsOC0zLjU4Miw4LThTMTQuNDE4LDIsMTAsMnoiLz48L3N2Zz4=)}
.u-svg{display:inline-block;vertical-align:middle;background-position:0 0;background-size:contain;background-repeat:no-repeat}
.m-input .u-svg-srch{position:absolute;left:0;top:9px;margin:0 8px;vertical-align:middle}
.input{outline:0}
input,select,textarea{-webkit-appearance:none;border-radius:0;border:0;background-color:transparent}
.m-input .input{width:100%;height:30px;line-height:18px;background:0 0;font-size:14px;color:#333}
.m-input .holder{position:absolute;left:30px;top:5px;font-size:14px;color:#c9c9c9;background:0 0;pointer-events:none}
label,summary{cursor:default}
.holder.active{display: none;}
.m-input .close{position:absolute;right:0;top:0;width:30px;height:30px;line-height:28px;text-align:center}
.u-svg{display:inline-block;vertical-align:middle;background-position:0 0;background-size:contain;background-repeat:no-repeat}
.m-input .u-svg-empty{display:none;vertical-align:middle}
.m-input:after{border-color:rgba(0,0,0,.1)}
.f-bd:after{width:200%;height:200%;-webkit-transform:scale(.5);transform:scale(.5)}
.m-hotlist{padding:15px 10px 0}
.m-hotlist .title{font-size:12px;line-height:12px;color:#666;text-align:left;}
.m-hotlist .list{margin:10px 0 7px}
.m-hotlist .item{display:inline-block;height:32px;margin-right:8px;margin-bottom:8px;padding:0 14px;font-size:14px;line-height:32px;color:#333}
.f-bd{position:relative}
.m-hotlist .item:after{border-color:#d3d4da;border-radius:32px}
.f-bd:after{width:200%;height:200%;-webkit-transform:scale(.5);transform:scale(.5);border-bottom:1px solid  rgba(0,0,0,.1)}
.u-svg-empty{width:14px;height:14px;background-image:url(data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHZpZXdCb3g9IjAgMCAyOCAyOCI+PGcgZmlsbC1ydWxlPSJldmVub2RkIj48cGF0aCBmaWxsPSIjYmNiZGJkIiBkPSJNMTQsMGM3LjczMiwwLDE0LDYuMjY4LDE0LDE0YzAsNy43MzItNi4yNjgsMTQtMTQsMTQKCVMwLDIxLjczMiwwLDE0QzAsNi4yNjgsNi4yNjgsMCwxNCwweiIvPjxnIGZpbGw9Im5vbmUiIHN0cm9rZT0iI2ViZWNlYiIgc3Ryb2tlLXdpZHRoPSIyLjUiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCI+PHBhdGggZD0ibTE5IDlsLTEwIDEwIi8+PHBhdGggZD0ibTkgOWwxMCAxMCIvPjwvZz48L2c+PC9zdmc+)}
.u-svg{display:inline-block;vertical-align:middle;background-position:0 0;background-size:contain;background-repeat:no-repeat}
.m-input .u-svg-empty.z-show{display:inline-block}
.m-input .u-svg-empty.z-show{display: inline-block;}
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
.m-sglst.active{display: none}
.m-sglst li{padding-left:10px}
.m-sglst li, .sgfl {display: -webkit-box;display: -webkit-flex;display: flex;}
.m-sglst li a{display:flex;width:100%}

</style>