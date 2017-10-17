<template>
  <div class="wrapper">
     <div class="float-bar" >  
                <router-link to="/Home">
                    <i class="fa fa-arrow-left"><img src="../assets/images/back.png"/></i>                
                </router-link>
                <span class="index">av{{Detail.episodes[0].av_id}}</span>
                 <mu-icon-menu icon="more_vert" slot="right" >
                    <mu-menu-item title="添加到稍后再看"/>
                    <mu-menu-item title="不感兴趣"/>
                    <mu-menu-item title="稿件投诉"/>
                    <mu-menu-item title="设置"/>
                    <mu-menu-item title="播放问题反馈"/>
                </mu-icon-menu> 
      </div> 
      <video controls="controls" :src="videoSrc"  class="video" autoplay="autoplay" />  
      <div class="option">
          <div class="option-item"><img src="../assets/images/分享.png" /><span>分享</span></div>
          <div class="option-item"><img src="../assets/images/尼玛币.png" /><span>{{Detail.coins}}</span></div>
          <div class="option-item"><img src="../assets/images/追番数_32.png" /><span>收藏</span></div>
          <div class="option-item"><img src="../assets/images/下载1.png" /><span>缓存</span></div>
      </div>                
      <div class="Anthology">
            <span>选集</span>
            <span class="new">更新至第 {{Detail.newest_ep_index}} 话 ></span>
      </div>
      <div class="anthology_part">
          <ul class="list" >
              <li class="part"  v-for="item in Detail.episodes" @click="showIndex(item.index)">
                      <p class="part_name" >第{{item.index}}话</p>
                      <p class="part_title" >{{item.index_title}}</p>
              </li>                
          </ul>
      </div>
      <div class="showInfo">
          <div class="playinfo">
              <p class="title">{{Detail.bangumi_title}}</p>
              <p class="update">{{Detail.episodes[0].is_new}}天前更新</p>
              <p class="desc">弹幕数：{{Detail.episodes[0].danmaku}}</p>            
              <p class="desc">{{Detail.evaluate}}</p>
          </div>
              <div class="tagAll"> 
                    <p class="tagAbout">视频相关标签</p> 
                    <span class="tag" v-for="tag in Detail.tags">{{tag.tag_name}}</span>                   
              </div>
     </div>
     <div class="ShowComment" >
              <p class="comment">评论 <span>({{comment.length}})</span></p>
              <ul class="cmtList">
                  <li v-for="(cmt, index) in comment">
                      <img :src="cmt.member.avatar" alt="" class="avatar">
                      <span class="name">{{cmt.member.uname}}</span>
                      <p class="comment">{{cmt.content.message}}</p>
                  </li>
              </ul>
              <div style="width:100%; text-align: center; margin-top: 1rem; margin-bottom: 10rem; color: grey;">
                    _(•̀ω•́ 」∠)_再怎么下拉也没有啦......
                </div>
            <div class="talk">
                <img src="../assets/images/emoji.png" class="emoji"></img>
                <input type="text" v-model="cmtContent" @keypress.enter="submitCmt"  placeholder="说点什么">
                <img src="../assets/images/send.png" class="send" @click="submitCmt">
            </div>
          </div>
  </div> 
</template>

<script>
export default {
    name:'cartoonPlay',
   data() {
       return {
            videoSrc: '',
            Detail: '',
            comment: [ ],
            cmtContent: '',
            index: 1,
            Detail: {
                episodes: [{
                    is_new:[],
                    danmuku: []
                }]
            }
       }
   },
   mounted() {
         let season_id =  this.$route.params.season_id
         this.axios.get('https://api.imjad.cn/bilibili/v2/?season_id=' + season_id + '&page=1&quality=2&index=1').then((res) => {                    
             this.videoSrc = res.data.durl[0].url
             }).catch((error) => {
                console.log(error)
        })
        this.axios.get('https://api.imjad.cn/bilibili/v2/?get=seasoninfo&season_id=' + season_id ).then((res) => {
                this.Detail = res.data.result
             }).catch((error) => {
                console.log(error)
        })
        this.axios.get('https://api.imjad.cn/bilibili/v2/?get=comments&season_id=' + season_id ).then((res) => {
                this.comment = res.data.data.replies
             }).catch((error) => {
                console.log(error)
        })
  },
  methods: {
     showIndex(index) {
         this.index = index
         let season_id =  this.$route.params.season_id
         this.axios.get('https://api.imjad.cn/bilibili/v2/?season_id=' + season_id + '&page=1&quality=2&index=' + index).then((res) => {
             console.log(index)
             console.log(res.data)
                 this.videoSrc = res.data.durl[0].url     
             }).catch((error) => {
                console.log(error)
        })
     }
  }
}
</script>

<style lang="css" scoped>
* {
    margin:0;
    padding:0;
}
video {
    margin-top: 3.5rem;
}
.float-bar {
    position: fixed;
    z-index: 9999;
    width: 100%;
    display: flex;
    color: #fff;
    background-color: #FA7198;
    height: 3.5rem;
}
.fa-arrow-left {
    display: block;
    margin-left: 1rem;
    margin-top: 1rem;
    margin-right: 3rem;
    
}
.fa-arrow-left img {
    width:1.5rem;
    height: 1.5rem;
}
.fa-arrow-left .span {
    z-index: 99;
    position: absolute;
    margin-top: .75rem;
    margin-left: 5rem;
}
.index {
    text-align: center;
    margin: 0 auto;
    margin-left: 1.5rem;
    height:3.5rem;
    line-height:3.5rem;
    font-size: 1.2rem;
}

video {
    width: 100%;
    height: 30%;
    background-color: black;
}
.Anthology {
    padding-top: 1rem;
    padding-left: .7rem;
    background-color: #fff;
}
.new {
    position: absolute;
    right: 1rem;
    color: #9c9c9c;
}

.anthology_part {
    height: 8rem;
    width: 100%;
    overflow-y: hidden;
    overflow-x: scroll;  
    position: relative;  
    margin-bottom: 0.5rem;
    background-color: #fff;
}
.anthology_part ul {
    list-style: none;  
    width:4000rem;  
    display: flex;
    margin-top: 1.5rem;
    margin-left: 0.7rem;
}
.anthology_part ul li {
    border: 1px solid #FA7198;
    width: 9rem;
    height: 5rem;
    background-color: #FAFAFA;
    border-radius: .7rem;
    padding: .6rem;
    color: #9c9c9c;
    font-size: 1.5rem;
    margin-right: 1rem;
}
.part_name {
    margin-bottom: .2rem;
    font-size:0.85rem;
}
.part_title {
    overflow-y: hidden;
    white-space: nowrap;
    text-overflow : ellipsis ;
    font-size: 1rem;
}

.showInfo {
    padding-top: .5rem;
    margin-top: 1rem;
    background-color: #fff;
}
.showInfo .title {
    margin-left: .7rem;
    font-size: 1.5rem;
    margin-bottom: .5rem;
    font-size: 1rem;
    font-weight: 700;
}
.showInfo .desc {
    margin-left: .7rem;
    color: #9c9c9c;
    width: 96%;
    margin-bottom: .7rem;
}
.showInfo .tagAbout {
    font-size: 1.5rem;
    margin-left: .7rem;
    margin-bottom: 1rem;
    font-size: 1rem;
}
.showInfo .tag {
    border:1px solid #9c9c9c;
    background-color: #fff;
    border-radius: .9rem;
    padding-left: .7rem;
    padding-right: .7rem;
    padding-top: .1rem;
    padding-bottom: .1rem;
    margin-left: .5rem;            
}

.comment {
    margin-top: 1rem;
    margin-left: .7rem;
    padding-top: .5rem;
    margin-bottom: 1rem;
    font-size: 1rem;
}
.comment span {
    margin-left: .3rem;
    color: #9c9c9c;
}
 .cmtList {
    display: flex;
    flex-direction: column;
    padding-bottom: 1rem;
    /* padding-bottom: 4.5rem; */
 }
.cmtList li {
    border-bottom: 1px solid #AFAFAF;
    color: #AFAFAF;
    list-style-type:none;
}
.cmtList li .avatar {
    width: 4rem;
    height: 4rem;
    border-radius: 50%;
    margin-top: 1.0rem;
    margin-left: 1.0rem;
    margin-bottom: -2.6rem;
}
.cmtList li .name {
    color: #FA7198;
    margin-left: .9rem;
}
.cmtList li .ico {
    float: right;
    margin-right: 1.7rem;
    margin-top: 1.4rem;
}
.cmtList li .ico  .fa {
    margin-right: .5rem;
}

.cmtList li .comment {
    margin-left: 6rem;
    margin-top: 1rem;
    margin-bottom: 1rem;
    color: #000;
}
.talk {
    position: fixed;
    bottom: 0;
    left: 0;
    right: 0;
    width: 100%;
    margin-top: 3rem;
    height: 4.5rem;
    line-height: 4.5rem;
    background-color: #FAFAFA; 
    margin-bottom:3rem;
}
.talk .emoji {
    left: .3rem;
    margin-top: .7rem;
}
.talk input {
    outline: none;
    border: 0;
    background-color: #FAFAFA;
    border-bottom: 1px solid #FA7198;
    width: 72%;
    position: relative;
    top: -1.4rem;
    height: 2.5rem;
}
.talk .send {
    margin-left: .3rem;
}
.option {
    width:100%;
    height: 3rem;
    line-height: 3rem;
    display: flex;
    border-bottom: 1px solid #9c9c9c;
    text-align: center;
    vertical-align: center;
    vertical-align: middle;
    background-color: #fff;
}
.option-item {
    flex: 1;
    color: #9c9c9c;
}
.option-item img{
    width:1.5rem;  
    height: 1.5rem;
    line-height: 1.5rem;
    vertical-align: middle;
    margin-right:0.5rem; 
}
.playinfo{
    border-bottom: 0.5rem solid #f1f1f1;
    margin-bottom: 0.5rem;
}
.tagAll {
    padding-bottom: 0.5rem;
}
.update {
    margin-left: .7rem;
    color: #9c9c9c;
    width: 25%;
    margin-bottom: .7rem;
    float: right;
}
</style>