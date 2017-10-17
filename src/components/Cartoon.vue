<template>
  <div>
    <div class="pageheader">
        <div class="tagcontainer">
            <div class="fanju">番剧</div>
            <div class="guangchuang">国创</div>
        </div>
        <div class="smalltitle">
            <div class="timetable"><img src="../assets/images/时间表.png"/>时间表</div>
            <span>丨</span>
            <div class="index"><img src="../assets/images/索引.png"/>索引</div>
        </div>
    </div>
    <div class="pagecontent">
      <p class="totalRecommond">
          <img src="../assets/images/我的追番.png" alt="">
          <span class="recommond">新番推荐</span>
          <span class="right">more >></span>
      </p>
      <div class="show-content">
        <div class="showItem col-xs-4" @click="Detail(item.season_id)"  v-for="item in dramaList" >
            <img :src="item.cover" alt="" class="showImg">    
            <div class="showInfo">
                <span class="showTitle">{{item.title}}</span>  
                <p class="showNum">更新至第{{item.newest_ep_index}}话</p>
                <p class="showNum">全{{item.total_count}}话</p>
            </div>
       </div>
      </div> 
      <div style="display:inline-block;width:100%; text-align: center; margin-top: 1rem; margin-bottom: 4.5rem; color: grey;">
        _(•̀ω•́ 」∠)_再怎么下拉也没有啦......
      </div>
    </div>
  </div>
</template>
<script>
export default {
  name: 'v-cartoon',
  data() {
      return {

      }
  },
  computed: {
        dramaList () {
            return this.$store.state.dramaList
        }
    },
    created () {
         this.axios.get('https://api.imjad.cn/bilibili/v2/?get=rank&content=global')
            .then (res => {    
                this.$store.state.dramaList = res.data.result.list;
         })
    },
     methods: {
          Detail(season_id) {
            this.$router.push(
                 {name: 'cartoonPlay', params: {'season_id': season_id}}
             )
        }
    }
}
</script>
<style scoped>
* {
    margin: 0;
    padding: 0;
}
.pageheader {
    background-color: #fff;
    margin-bottom: 1rem;
}
.pagecontent {
    width: 100%;
}
.tagcontainer {
    width: 100%;
    display: flex;
    text-align: center;
    vertical-align: middle;
    vertical-align: center;
    font: 1.2rem sans-serif;
    color:#fff;
    padding-top:1rem;
    padding-bottom:1rem;
    justify-content:center;
    border-bottom: 1px solid #F4F4F4; 
}
.fanju {
    width: 7rem;
    height: 3rem;
    line-height: 3rem;
    border-radius: 8%;
    margin-right:1rem;
    background: linear-gradient(45deg,#BBFFFF 25%,#87CEFF 0,#87CEFF 50%,#BBFFFF 0,#BBFFFF 75%,#87CEFF 0);
    background-size: 2rem 2rem;
}
.guangchuang {
    width: 7rem;
    height: 3rem;
    line-height: 3rem;
    border-radius: 8%;
    background: linear-gradient(to right,#FF7256 55%,#FF6347 55%);
    background-size: 2rem 2rem;
}
.smalltitle {
    display: flex;
    justify-content:center;
    text-align: center;
    height: 2rem;
    line-height: 2rem;
}
.smalltitle span {
    padding: 0 2rem;
    color:#F4F4F4;
}
.timetable {
    height: 1.2rem;
    text-align: center;
}
.timetable img {
    height: 1.2rem;
    width: 1.2rem;
    margin-right: 1rem;
    vertical-align: middle;
}
.index {
    height: 1.2rem;
}
.index img {
    height: 1.2rem;
    width: 1.2rem;
    margin-right: 1rem;
    vertical-align: middle;
}
.totalRecommond {
    height: 20%;
    padding-top: 1rem;
    margin-bottom: .6rem;
    background-color: #fff;
}
.totalRecommond img {
    vertical-align: middle;
    margin-left: .5rem;
}
.recommond {
    margin-left: .5rem;
}
.right {
    float: right;
    margin-top: .45rem;
    margin-right: .98rem;
    font-size: .8rem;
    color: #4f4f4f;
}
.show-content {
    width: 100%;
    position: relative;
    background-color: #fff;
    padding-left: 3.5%;
}
.show-content .col-xs-4 {
    width: 30%;
    float: left;
    position:relative;
}
.show-content .showItem {
    height: 12rem;
    margin-right: 3%;
    margin-bottom: 3%;
    background-color: transparent;
    border-radius: 3px;
    border:1px solid #f2f2f2;
    display: flex;
    flex-direction: column;
    background-color: #fff;
    font-size: 0.8rem;
}
.showItem img {
    width: 100%;
    height: 60%;
    background-size: cover;
}
.showInfo {
     margin-top: .5rem;
}
.showNum {
    margin-top: .1rem;
    color: #9c9c9c;
}
.showTitle {
    display:-webkit-box;
    -webkit-line-clamp: 1;
    -webkit-box-orient: vertical;
    overflow: hidden;
}
</style>