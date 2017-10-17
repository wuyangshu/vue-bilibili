<template>
<div>
<div class="grid" v-for="item in liveList">
    <div class="grid-container" >
        <img class="grid-img" v-lazy="item.pic" />
        <div class="info">
            <div class="info-playIcon">
                <img src="../assets/images/播放数_32.png"/>
            </div>
            <div class="info-play">
                <p>{{item.play}}</p>
            </div>
            <div class="info-danmuIcon">
                <img src="../assets/images/弹幕数_32.png"/>
            </div>
            <div class="info-danmu">
                <p>{{item.video_review}}</p>
            </div>
            <div class="time">{{item.duration}}</div>
        </div>
    </div>
    <div class="grid-title-container">
        <p class="title">{{item.title}}</p>
        <p class="s-title">{{item.author}}
        <mu-icon-menu icon="more_vert" :anchorOrigin="leftBottom" :targetOrigin="leftBottom">
        <mu-menu-item title="添加到稍后再看" />
        <mu-menu-item title="使用小窗播放" />
        <mu-menu-item title="不感兴趣" />
        </mu-icon-menu>
        </p>
    </div>
</div>
</div>
</template>
<script>
export default {
  name:'v-gridtv',
  data () {
    return {
      leftBottom: {horizontal: 'left', vertical: 'bottom'}
    }
  },
  computed: {
        liveList () {
            return this.$store.state.liveList
        }
    },
   created () {
         this.axios.get('https://api.imjad.cn/bilibili/v2/?get=rank&content=160')
            .then (res => {    
                this.$store.state.liveList = res.data.rank.list;
         })
         .catch(function (error) {
                    console.log(error);
                })
    }
}
</script>
<style lang="css">
.mu-paper {
    z-index:9999999;
}
.grid {
    display: block;
    text-decoration: none;
    position: relative;
    width: 50%;
    float: left;
    margin-bottom: .68267rem;
}
.grid .grid-container {
    position: relative;
    width: 90%;
    height: 5.52267rem;
    overflow: hidden;
    display: block;
    margin: auto;
    border-radius: .256rem .256rem 0 0;
    background-color: #e7e7e7;
    z-index: 1;
    background-image: linear-gradient(transparent 50%,rgba(0,0,0,.5))
}
.grid .grid-container .grid-img {
    position: absolute;
    top: 0;
    z-index: 2;
}
.grid .grid-container img {
    display: block;
    width: 100%;
}
.grid .grid-container img[lazy=loading] {
    display: block;
    width: 100%;
}
.grid .grid-container .info {
    position: absolute;
    z-index: 3;
    left: 0;
    padding-left: .34133rem;
    width: 100%;
    bottom: 0;
    height: .98267rem;
    background: linear-gradient(180deg,rgba(33,33,33,0),rgba(33,33,33,.5));
}
.info-playIcon {
    position: relative;
    float: left;
    width: 1.08267rem;
    margin-top: -.264rem;
}
.info-playIcon img{
    display: block;
    width: 100%;
    height:1.08267rem;
}
.info-play {
    position: relative;
    float: left;
    margin-left: .156rem;
    width: 2.048rem;
    margin-top: 0.104rem;
}
.info-play p{
    text-align: left;
    font-size: .46933rem;
    color: #fff;
    line-height: .59733rem;
}
.info-danmu {
    position: relative;
    float: left;
    margin-left: .156rem;
    width: 2.048rem;
    margin-top: 0.104rem;
}
.info-danmu p{
    text-align: left;
    font-size: .56933rem;
    color: #fff;
    line-height: .59733rem;
}
.info-danmuIcon {
    position: relative;
    float: left;
    width: 1.08267rem;
    margin-top: -.264rem;
}
.info-danmuIcon img{
    display: block;
    width: 100%;
    height:1.08267rem;
}
.grid-title-container {
    width: 90%;
    position: relative;
    margin: auto;
    /* margin-top: .21333rem; */
    height: 3.52267rem;
    overflow: hidden;
    background-color: #fff;
    border-radius: 0 0 .256rem .256rem ;
}
.grid-title-container p {
    /* font-size: .55467rem; */
    color: #212121;
    letter-spacing: 0;
    line-height: .68267rem;
    text-align: left;
}
.time {
    z-index: 1000;
    text-align: right;
    font-size: .76933rem;
    color: #fff;
    height: .78267rem;
    line-height: .78267rem;
    margin-top: -0.1rem;
}
.grid-title-container .title {
    font-size: .70267rem;
    line-height: .70267rem;
    height: .70267rem;
    padding-left: .59733rem;
    margin-top: .49733rem;
    display:-webkit-box;
    -webkit-line-clamp: 2;
    -webkit-box-orient: vertical;
    overflow: hidden;
}
.grid-title-container .s-title {
    float: left;
    font-size: .76933rem;
    margin-top: 1.10733rem;
    margin-left: .39733rem;
    color: #9c9c9c;
}
.mu-icon-menu {
    float: right;
    height: .56933rem;
    width: .56933rem;
    margin-top: -1.19733rem;
    margin-left: 2.79733rem;
}
.mu-icon {
    font-size: 1.1rem;
    cursor: inherit;
}
</style>
