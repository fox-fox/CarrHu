<template>
    <div class="Details">
        <div class="m-song-bg" :style="{backgroundImage: 'url(' + $route.params.list_pic + ')'}"></div>
        <div class="m_bg"></div>
        <div class="m-song_newfst">
            <div class="m-song-wrap">
                <div class="m-song-disc">
                    <div class="m-song-turn" :class="{active : toClass == true}">
                        <div class="m-song-rollwrap">
                            <div class="m-song-img ">
                                <img class="u-img" :src="$route.params.list_pic" alt="">
                            </div>
                        </div>
                    </div>
                    <div class="m-song-plybtn" v-show="toggleShow"></div>
                </div>
                <div class="m-song-clickarea" @click="Switch"></div>
                <div class="m_audio" ref="audioo">
                    <audio id="audio" :src="$route.params.list_url" autoplay controls="controls"></audio>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
export default {
    data(){
        return{
            toggleShow:false,
            toClass:false,
            status:true
        }
    },
    methods:{
        Switch:function(){
            this.toggleShow = this.toggleShow ? false : true;
            this.toClass = this.toClass ? false : true;
            var self = this;
            var audio =document.querySelector('#audio');
            if(self.status == false) {     //初始状态未播放，点击播放
                audio.play();
                self.status = true
            }else{                  //已经在播放，点击暂停
                audio.pause();
                self.status = false
            }
        }
    }
}
</script>



<style scoped>
.m_audio{position:absolute;z-index:-10;opacity:0}
.m_bg{position: absolute;left: 0;top: 0;width: 100%;height: 100%;z-index: 1;background: #170e0b;opacity: 0.5;}
.Details{height: 100%;position: absolute;left:0;top:0;width: 100%;}
.m-newsong,.m-song{position:absolute;top:0;left:0;right:0;bottom:0;min-width:320px;overflow:hidden}
.m-song-bg{background-position:50%;background-repeat:no-repeat;background-size:auto 100%;-webkit-transform:scale(1.5);transform:scale(4.2);-webkit-transform-origin:center top;transform-origin:center top;position:fixed;left:0;right:0;top:0;height:100%;overflow:hidden;z-index:-1;-webkit-transition:opacity .3s linear;transition:opacity .3s linear;opacity:1}
.m-song_newfst{position:relative;padding-bottom:12px;box-sizing:border-box;height:100%}
.m-song-wrap{padding-top:70px;overflow: hidden;}
.m-song-disc{position:relative;width:296px;height:296px;margin:0 auto;z-index: 20;}
.m-song-turn:before{content:" ";position:absolute;left:0;right:0;top:0;bottom:0;z-index:2;background-image:url(//s3.music.126.net/m/s/img/disc-ip6.png?6979612…);background-size:contain}
.m-song-rollwrap{position:absolute;left:50%;top:50%;z-index:1;width:184px;height:184px;margin:-92px 0 0 -92px}
.m-song-plybtn{position:absolute;width:56px;height:56px;left:50%;top:50%;-webkit-transform:translate(-50%,-50%);transform:translate(-50%,-50%);z-index:10;background:url(data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAAKgAAACoCAMAAABDlVWGAAABJlBMVEUAAAAAAAD////l5eX///9iYmKDg4Pn5+f///9YWFj////09PT////4+Pjt7e3///////9oaGhBQUH////////////////CwsIaGhr///8xMTEkJCT////7+/vp6en///////////////+srKyoqKienp58fHz////y8vKTk5P///8EBAT////////////////V1dW3t7f////////////////////v7++jo6N9fX3///////+UlJT////s7Oz////Nzc3///////+RkZGPj495eXkTExP////////29vb////k5OTPz882Njb////////////c3Nz///////9ycnJsbGz///9dXV3////////Q0ND///9QUFD///////////////////9FeiN6AAAAYXRSTlNmAP3c+oWT3ueB9vA19ealRId5EQbuurpu83RxD/nh05dfAquooo+M7JtzaSolE+vMspJ3Wj7w6KSQj6ucKeXNxLWnmpmObVYd8t3axXZRSt7TvbKLideCeSzHnn4V3Nh6YarbPAAABlRJREFUeNrU14lWEmEYh/GXcdj3HQTZRCkS913UNE2zbLd9Oc/930Q2LmVpwPAC03MD/M5835n/IC6dkqHnzcVoZvdkLp2HfHruZDcTXWw+DyVdOilAt6uNjI8782Ua1W2XjTShtdDSmzRdlH6zFKq5bKQBTS5H57gqXJrP1tsb7kShkBPJFQoJ90a7np0vhblqLrrc8R7oQ4vVPZOLIp8mp8flzsanJ59FuMjcqxZdHVKFxvYDWK1lPQXpooInu4ZVYD/m6pAWNLn0DSvvekJ6KLHuxerb0qyrQwrQViV/oZzKSc/lpi6sgUrLdSN16MyWARBcOBWbnS4EAYytj67r1KGtqMUseaSvPCWLGr14u+pDZysmwFhc+i4+BmBWZgcATTXTFvO9qOS3qOlmShu68g7A6xa13F6A7yuq0ORnA9jZENU2dgDjc1IPGvMB4QNR7+AJ4IspQVObBjDmF+Wur6qxmdKAbpeBoEcGlCcIlLf7hx7lOzxOlYeaP+oTmmoYQFsGWhswGql+oMUMEInLgItHgEzRPvS43OHYVY+/fGwXGvIBkzKU6oAvZA8aywOPZEg9AvIxO9AXAZg4lKF1OAGBF71DX5jw5EyG2NkTMJ/3Co2ZcM8tQ819D8xYb9CVgA2nijSw0gs0tArBzk59aRBWQ91Dj30QjssIiofBd9wttFiGiTMZSWcTUC52B629Bg5lRB0Cr2tdQRvAfRlZ94FGN9AjA+oywupgHHWGzuRhTEbaGORnOkFTZYj4ZaT5I1BOdYBuAnEZcXFg89/QmAFtGXltMGL/ghZ9I7+g19fUV/wHtAJBvzggfxAqd0NXDPCII/KAsXIXNPXOIQd/efjvUndAmxB2xMH/zB+G5u3Qr2k4EMd0AOmvt0IrsCMOagcqt0FbJkyLg5oGs3ULNApecVReiP4NnTHALY7KDcbHv6BbDno1XTUGW39CWwa8F4flB6P1B3TRgQ/UeqSLN6GzAQd83f1dHAKzN6AfoCQOrARLN6Andr9GpiITT9/KwPLAye/QGATFTusAxsOCDKogxH6D7sOC2GkNq+B9GVALsP8LWgzAqdjJ4LJXCRlIpxAoXkOrtteT6yYmH8gg8kL1GroHU/1CoTSQBZ6CvSto0oRc/1DM7GNRLwdm8hK6DF5RgMI9j6jnheVLaBTWdaAwPy7KrUP0Alqbg4QWlPCU6JaAuZoFDcGaqEHh6RdRLQIhC/oBsppQzAXVN1UWlixoBjyqUIhozr8H3vyE1lYhpwnVnv8CpH9CZyAi2lAIPtK8pDPn0Cp8UoWqz/8zqJ5DGzCpCdWf/0lonEMzMK0J1Z//acicQ30wrgnVn/9x8LkkCWFRherPfxiSEgKvLlR//r0QkmWY14Xqz/88LEsTsqpQ/fm3RlQWoa4L1Z//OixKFNq6UP35vw9RycDGMKAYD3P9vEhlF9y6UP35d8OuvISELlR//hPwUqxh0oTqz781TbIKueFB4em4rb/Mq5IfMpRn0nOPIS+ADBUatvcz/w/0B/X2VgMACMNQ9AMnWOADKwT/QuahyZYcDcte7e146X9W+vFmWmEzOeOJGfjMCmWOEubMYw7no7wizHPHvMuMAMFIOo5IxsiOjJDLSOOM2cDYN44hxliMjGnL2OAOWMCgGgz84uBEDKDFIG8ORLhzLPO2Y5kK6PpMdJiBsR28nQkMOBEMJtTixISY4JUTZWPCgVXevesgCINhGG7dZPLEIg7GRRsMTsaoMTEOnmLUuBgn+e//JuTHGt0aKT3y3QIFpj6vO9ctnbnAmr9PIysefn0E0PfhkjW92HFtnQHULn5AAG9aISZGF3NaQYxVrInRrcVYBW4H5vkPEPIfuIV5UGXhClHT8Qv9oXQ/MckoTfb+wVTGqK8ZUl9+4mmUnpGj03pOmzlH5y/w5w6ZiAil+G9qA0KpkfWMTxKsJ6530wel3try9CwjSscg27BTDcw321gHjzyuEjj9IbwP1hPeDqHo2abP0pn5XMR/NhTB/fyo2gv3q0gh1JSkEHCrUuMSG1VxCdxDOtfR1ZDr4AGUwIUACi5JJZMyx1RHUgY3kIn0LBuFQk2EFlv7J3t0+id7JPi86wlJsfm9FUVbQrZR1LrPmQ0hKZfSXC7Fzr5LeD7uGoYBQBCGV56PS2g5ewGy+NkUNbjr9gAAAABJRU5ErkJggg==) 0 0 no-repeat;background-size:contain}
.m-song-plybtn:after{content:"";display:block;position:absolute}
.m-song-disc:after{content:" ";position:absolute;z-index:5;background:url(//s3.music.126.net/m/s/img/needle.png?702cf6d…) no-repeat;background-size:contain;width:96px;height:137px;top:-70px;left:133px;background-image:url(//s3.music.126.net/m/s/img/needle-ip6.png?be4ebbe…)}
.m-song-clickarea{position:absolute;width:100%;top:0;left:0;bottom:150px;z-index:30}
.m-song-bg:after{content:" ";position:absolute;left:0;right:0;bottom:0;top:0;background-color:rgba(0,0,0,.5)}
.m-song-img{width:100%;height:100%;border-radius:50%;overflow:hidden;background:url(//s3.music.126.net/m/s/img/disc_default.png?7c9b3ad…) no-repeat;background-size:contain}
.u-img{width:100%;vertical-align:middle}
.m-song-turn{animation: mymove 20s linear infinite;width:100%;height:100%;animation-play-state:running;}
.m-song-turn.active{animation-play-state:paused;}
@keyframes mymove{from{transform:rotate(0)}
to{transform:rotate(360deg)}
}
</style>

