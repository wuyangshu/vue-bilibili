<template lang="html">
<div class="headpage">
  <mu-popup position="left" popupClass="demo-popup-left" :open="leftPopup" @close="close('left')">
        <div class="b-sidebar">
                <div class="b-user">
                    <img src="../assets/images/avatar.jpg" alt="">                    
                    <div class="icon" style="color: white">
                        <i class="fa fa-wallet"></i>   
                        <i class="fa fa-er"></i>
                    </div>  
                    <div class="user-desc">
                        <div>
                            <span class="user-username">血色如故</span>
                            <span class="user-grade">LV4</span>
                            <span class="user-vip">正式会员</span> 
                        </div>                                                           
                        <div class="user-money">
                            <span class="user-coin">硬币：  576.00</span>
                            <span class="user-bcoin">B币：  0.0</span>
                        </div> 
                    </div>                    
                </div>
                 <div class="b-sideItem">
                    <ul class="side-List">
                        <mt-cell-swipe title="首页"  >
                             <span></span>
                             <img class="tag" slot="icon" src="../assets/images/首页.png">
                        </mt-cell-swipe>
                        <mt-cell-swipe title="历史记录"  >
                             <span></span>
                             <img class="tag" slot="icon" src="../assets/images/历史记录.png" width="24" height="24">
                        </mt-cell-swipe>
                         <mt-cell-swipe title="离线缓存"  >
                             <span></span>
                             <img class="tag" slot="icon" src="../assets/images/下载缓存.png" width="24" height="24">
                        </mt-cell-swipe>
                         <mt-cell-swipe title="我的收藏"  >
                             <span></span>
                             <img class="tag" slot="icon" src="../assets/images/我的收藏.png" width="24" height="24">
                        </mt-cell-swipe>
                         <mt-cell-swipe title="我的关注">
                             <span></span>
                             <img class="tag" slot="icon" src="../assets/images/我的关注.png" width="24" height="24">
                        </mt-cell-swipe>
                        
                         <mt-cell-swipe title="稍后再看"  >
                             <span></span>
                             <img class="tag" slot="icon" src="../assets/images/稍后再看.png" width="24" height="24">
                        </mt-cell-swipe>
                        <hr class="limite"></hr>
                         <mt-cell-swipe title="直播中心"  >
                             <span></span>
                             <img class="tag" slot="icon" src="../assets/images/智能电视.png" width="24" height="24">
                        </mt-cell-swipe>
                         <mt-cell-swipe title="我的大会员"  >
                             <span></span>
                             <img class="tag" slot="icon" src="../assets/images/我的大会员.png" width="24" height="24">
                        </mt-cell-swipe>
                         <mt-cell-swipe title="免流量服务"  >
                             <span></span>
                             <img class="tag" slot="icon" src="../assets/images/免流量服务.png" width="24" height="24">
                        </mt-cell-swipe>
                        <mt-cell-swipe title="会员购订单"  >
                             <span></span>
                             <img class="tag" slot="icon" src="../assets/images/订单.png" width="24" height="24">
                        </mt-cell-swipe>
                     </ul>    
                </div>
            </div> 
            <div class="b-footer">
                <div class="icon" style="color: #7f7f7f">
                    <i class="fa fa-config"></i><span>设置</span> 
                    <i class="fa fa-theme"></i><span>主题</span> 
                    <i class="fa fa-night"></i><span>夜间</span> 
                </div> 
            </div>
  </mu-popup>
  <div class="b-header" style="background: #fa7198">
          <i><img src="../assets/images/三杠.png" class="fa-bars" @click="open('left')"></i>
          <img src="../assets/images/avatar.jpg" @click="open('left')" class="b-avatar">
          <div class="right">
              <i class="fa"><img src="../assets/images/票.png"></i>
              <i class="fa"><img src="../assets/images/游戏.png"></i>
              <i class="fa"><img src="../assets/images/下载.png"></i>
              <router-link to="/Search">
              <i class="fa"><img src="../assets/images/搜索.png"></i>
              </router-link>
          </div>
          </div>
</div>
</template>
<script>
import vSearch from '@/components/Search.vue'
export default {
  name: 'vHeader',
  data () {
    return {
      leftPopup: false,
    }
  },
  methods: {
    open (position) {
      this[position + 'Popup'] = true
    },
    close (position) {
      this[position + 'Popup'] = false
    }
  },
  watch: {
    topPopup (val) {
      if (val) {
        setTimeout(() => {
          this.topPopup = false
        }, 2000)
      }
    }
  }
}

</script>

<style lang="css">
* {
    margin: 0;
    padding: 0;
}
.mu-avatar img {
  width: 1.5rem;
  height: 1.5rem;
}
.demo-popup-left {
  display: flex;
  width: 75%;
  max-width: 375px;
  height: 100%;
  align-items: center;
  padding: 24px;
}
.headpage {
    position: relative;
    height: 100%;
    width: 100%;
    top: 0;
    bottom: 0;
    right: 0;
    left: 0;
    overflow-x: hidden;
    background: #fa7198;
  }
.b-header {
  width: 100%;
  height: 3.5rem;
  line-height: 3.5rem;
  }
.b-avatar {
  height: 2.5rem;
  width: 2.5rem;
  line-height: 3rem;
  margin-left: 0.7rem;
  border-radius: 50%;
  border: 2px solid #fff;
  vertical-align: middle;
  cursor: pointer;
}
.fa {
    color: #fff;
  }
.fa-bars {
  height: 2rem;
  width: 1.5rem;
  line-height: 3rem;
  margin-left: -0.6rem;
  vertical-align: middle;
  }
.fa img {
    height: 1.5rem;
    width: 1.5rem;
    line-height: 1.5rem;
    margin-left: 0.5rem;
    margin-right: 0.5rem;
    vertical-align: middle;
    cursor: pointer;
  }
.right {
    float: right;
}
.right .fa-search {
    margin-right: 1.3rem;
}
.b-sidebar {
    position: fixed;
    top: 0;
    left: 0;
    height: 100%;
    width: 100%;
    z-index: 100;
    background-color: #fff;
    transform: translate3d(0, 0, 0);
    overflow: auto;
}
.b-user {
  position: relative;
  width: 100%;
  height: 24%;
  background-color: #fb7299;
  background-image: url(../assets/images/哔哩哔哩动画.png);
  background-repeat:no-repeat;
  background-attachment:fixed;
  background-position:61% 71%;
}
.b-user img {
    width: 3.7rem;
    height: 3.7rem;
    border-radius: 50%;
    margin-top: 1rem;
    margin-left: 1.5rem;
    border: .1rem solid white;
}
.b-user .icon {
    float: right;
    margin-right: 1rem;
    margin-top: 1rem;
}
.b-user .fa {
    display:inline-block;
    border-radius: 50%;
    border: .1rem solid white;
    padding: 0.9rem;
    text-align: center;
}
.b-user .fa-wallet {
    margin-right: 0.8rem;
    background:url(../assets/images/钱包.png) center no-repeat;
}
.b-user .fa-er {
    background:url(../assets/images/二维码.png) center no-repeat;
}
.user-desc {
    position: absolute;
    left: 1.3rem;
    bottom: 0.0005rem;
    width: 13rem;
    height: 4rem;
    line-height: 1.75rem;
}
.user-username {
    color: #fff;
    font-weight:500;
    margin-top: .2rem;
    margin-right: .2rem;
    font-size: 0.9rem;
  }
.user-grade {
    color: #fff;
    border-radius: .35rem;
    border: 1.7px solid #fff;
    padding-left: .2rem;
    padding-right: .2rem;
    font-size: 0.6rem;
    margin-right: .2rem;
}
.user-vip {
    background-color: rgba(255,255,255,.7);
    border: .05rem solid #fff;
    border-radius: .35rem;
    padding-left: .2rem;
    padding-right: .2rem;
    font-size: 0.7rem;
    color:#fa7198;
}
.user-money {
    color: #fff;
    font-size: 0.8rem;
    color: #EEE9E9;
} 
.user-coin {
  margin-right: 0.4rem; 
}
.b-sideItem {
    width: 100%;
    height: 100%;
    background-color: #FAFAFA;
    overflow: scroll;
}
.side-List {
    display: flex;
    flex-direction: column;
    width: 100%;
    height: 100%;
    position: relative;
    overflow: scroll;
}
.mint-cell {
    background-color: #fafafa;
    min-height: 40px;
}
.tag{
    margin-right: 1.5rem;
}
.mint-cell-title {
    margin-right: 1rem;
}
.mint-cell:active {
    background-color: #e9e9e9;
    color: #FA7198;
} 
.mint-cell-wrapper {
    background-image: none;
    margin-top: .5rem;
    margin-bottom: .5rem;
}

li {
  margin-top: .7rem;
  margin-bottom: .7rem;
}
 li:active {
    background-color: #e9e9e9;
    color: #FA7198;
} 
.mint-cell-wrapper img {
    margin-left: .7rem;
    margin-top: .2rem;
}
.subtitle {
    margin-left: 1.9rem;
}
.limite {
  width: 100%;
  height: 0.1rem;
  margin: 0.5rem 0;
  background-color: #E5E5E5;
  border: none;
}
.b-footer {
  position: fixed;
  bottom: 0;
  left: 0;
  width: 100%;
  height: 8%;
  border-top:0.1rem solid #E8E8E8;
  background-color: #FAFAFA;
  z-index:9999;
  text-align: center;
}
.b-footer .icon {
  height: 100%;
  width: 100%;
  justify-content:center;
  align-items:center;
  display:flex;
}
.b-footer .fa-config {
    /* margin-right: 0.8rem; */
    background:url(../assets/images/设置.png) center no-repeat;
}
.b-footer .fa-theme {
    background:url(../assets/images/主题.png) center no-repeat;
}
.b-footer .fa-night {
    background:url(../assets/images/夜间模式.png) center no-repeat;
}
.b-footer .fa {
  display:inline-block;
  border-radius: 50%;
  border: .1rem solid #7f7f7f;
  padding: 1rem;
  text-align: center;
}
.b-footer span {
  height: 8%;
  line-height: 8%;
  margin-left:0.3rem;
  margin-right:0.6rem;
  font-size: 0.9rem;
}
</style>
