<template>
  <div class="list">
   
    <top class="top" title="排行榜" backgroundcolor="white" color="red" ></top>
    <div class="top1"></div>
    <!-- <div class="four"></div> -->
    
          <router-link class="four" :to="'/bookinfo1/'+maleBook[0]._id+'/'+maleBook[0].author" tag="div">
                
                  <img class="img4" :src="`http://statics.zhuishushenqi.com${maleBook[0].cover}`" />
              
          </router-link>
      
   
  

    <van-tabs class="six" v-model="active">
      <van-tab class="aa" title="女生">
        <van-row class="bb">
          <van-col class="cc" span="6">
            <van-sidebar v-model="activeKey">
              <van-sidebar-item
                v-for="item in femalelist"
                :key="item.id"
                :title="item.title"
                @click="getrank(item._id)"
              />
            </van-sidebar>
          </van-col>
          <van-col class="dd" span="18">
            <van-row class="book" v-for="(item,idx) in femaleBook" :key="item.cover">
              <router-link :to="'/bookinfo1/'+item._id+'/'+item.author" tag="div">
                <van-col class="book1" span="5">
                  <img class="img" :src="`http://statics.zhuishushenqi.com${item.cover}`" />
                </van-col>
                <van-col span="1"></van-col>
                <van-col class="book1" span="18">
                  <div class="bookTwo1">
                    <h2>{{idx+1}}.{{item.title}}</h2>
                  </div>
                  <div class="bookTwo2">
                    <p>{{item.shortIntro}}</p>
                  </div>
                  <div class="bookTwo3">
                    <div>
                      <span>{{item.author}}</span>
                    </div>
                    <div>
                      <van-tag round>{{item.majorCate}}</van-tag>
                      <van-tag round>{{item.minorCate}}</van-tag>
                    </div>
                  </div>
                </van-col>
              </router-link>
            </van-row>

            <!-- <div v-for="item in femaleBook" :key="item.id">
                   
                   <div class="book">
                       <div class="bookOne"> <img :src="`http://statics.zhuishushenqi.com${item.cover}`" /></div>
                       <div class="bookTwo">
                           <div class="bookTwo1"><h4>1.是的</h4></div>
                           <div class="bookTwo2">发的方法对方的水电费是的冯绍峰水电费第三方</div>
                           <div class="bookTwo3"><span>天蚕土豆</span> <span>sdfsf</span></div>
                       </div>

                   </div>
                 
            </div>-->
          </van-col>
        </van-row>
      </van-tab>
      <van-tab class="aa" title="男生">
        <van-row class="bb">
          <van-col class="cc" span="6">
            <van-sidebar v-model="activeKey">
              <van-sidebar-item
                v-for="item in malelist"
                :key="item.id"
                :title="item.title"
                @click="getrank(item._id)"
              />
            </van-sidebar>
          </van-col>
          <van-col class="dd" span="18">
            <van-row class="book" v-for="(item,idx) in maleBook" :key="item.cover">
              <router-link :to="'/bookinfo1/'+item._id+'/'+item.author" tag="div">
                <van-col class="book1" span="5">
                  <img class="img" :src="`http://statics.zhuishushenqi.com${item.cover}`" />
                </van-col>
                <van-col span="1"></van-col>
                <van-col class="book1" span="18">
                  <div class="bookTwo1">
                    <h2>{{idx+1}}.{{item.title}}</h2>
                  </div>
                  <div class="bookTwo2">
                    <p>{{item.shortIntro}}</p>
                  </div>
                  <div class="bookTwo3">
                    <div>
                      <span>{{item.author}}</span>
                    </div>
                    <div>
                      <van-tag round>{{item.majorCate}}</van-tag>
                      <van-tag round>{{item.minorCate}}</van-tag>
                    </div>
                  </div>
                </van-col>
              </router-link>
            </van-row>
          </van-col>
        </van-row>
      </van-tab>
      <van-tab class="aa" title="出版">
        <van-row class="bb">
          <van-col class="cc" span="6">
            <van-sidebar v-model="activeKey">
              <van-sidebar-item
                v-for="item in picturelist"
                :key="item.id"
                :title="item.title"
                @click="getrank(item._id)"
              />
            </van-sidebar>
          </van-col>
          <van-col class="dd" span="18">
            <van-row class="book" v-for="(item,idx) in pictureBook" :key="item.cover">
              <router-link :to="'/bookinfo1/'+item._id+'/'+item.author" tag="div">
                <van-col class="book1" span="5">
                  <img class="img" :src="`http://statics.zhuishushenqi.com${item.cover}`" />
                  <!-- {{item._id}} {{item.author}} -->
                </van-col>
                <van-col span="1"></van-col>
                <van-col class="book1" span="18">
                  <div class="bookTwo1">
                    <h2>{{idx+1}}.{{item.title}}</h2>
                  </div>
                  <div class="bookTwo2">
                    <p>{{item.shortIntro}}</p>
                  </div>
                  <div class="bookTwo3">
                    <div>
                      <span>{{item.author}}</span>
                    </div>
                    <div>
                      <!-- {{item.author}} -->
                      <van-tag round>{{item.majorCate}}</van-tag>
                      <van-tag round>{{item.minorCate}}</van-tag>
                    </div>
                  </div>
                </van-col>
              </router-link>
            </van-row>
          </van-col>
        </van-row>
      </van-tab>
    </van-tabs>
  </div>
</template>
<script>
import axios from "axios";

export default {
  data() {
    return {
      active: 0,
      activeKey: 0,
      femalelist: [],
      femaleId: [],
      maleId: [],
      malelist: [],
      picturelist: [],
      maleBook: [],
      femaleBook: [],
      pictureId: [],
      pictureBook: [],
      blast: {}
    };
  },
  created() {
    this.getRanking();
  },
  beforeDestroy(){
    this.getBookId()
  },
  methods: {
    getBookId() {
     
      this.$store.commit('getBookId',"3")
    },

 
    getRanking() {
      axios.get("https://novel.juhe.im/rank-category").then(res => {
        this.blast = res.data.epub[0];

        console.log(res);
        this.femalelist = res.data.female;
        this.femaleId = res.data.female[0]._id;
        this.malelist = res.data.male;
        this.maleId = res.data.male[0]._id;
        this.picturelist = res.data.picture;
        this.pictureId = res.data.picture[0]._id;

        // console.log(fema)
        axios.get(`https://novel.juhe.im/rank/${this.femaleId}`).then(res => {
          console.log(res);
          this.femaleBook = res.data.ranking.books;
          console.log(this.femaleBook);
        });
        axios.get(`https://novel.juhe.im/rank/${this.maleId}`).then(res => {
          console.log(res);
          this.maleBook = res.data.ranking.books;
          console.log(this.maleBook);
        });
        axios.get(`https://novel.juhe.im/rank/${this.pictureId}`).then(res => {
          console.log(res);
          this.pictureBook = res.data.ranking.books;
          console.log(this.maleBook);
        });
      });
    },
    getrank(id) {
      axios.get(`https://novel.juhe.im/rank/${id}`).then(res => {
        console.log(res);
        this.femaleBook = res.data.ranking.books;
        this.maleBook = res.data.ranking.books;
        this.pictureBook = res.data.ranking.books;
        console.log(this.femaleBook);
      });
    }
  }
};
</script>
<style lang="less">
.top {
  width: 100%;
  height: 6%;
  position: absolute;
  left: 0;
  top: 0;
  z-index: 10000;
}
.top1 {
  height: 6%;
} 
.mint-header-title {
  color: black;
}
.list {
  // position: absolute;
  height: 100%;
  //   overflow: hidden;
}
.four {
  // padding: 25px;
  padding-right: 10px;
  padding-left: 10px;
  
  width: 100%;
  height: 29%;
  box-sizing: border-box;
  // background-color: red;
  //  overflow: auto;
}
.list .pageHS {
  top: 40px
}
 .img4  {
  width: 100%;
  height: 100%;
}
.banner1 {
  height: 50%;
}
.six {
  height: 75%;
}
.aa,
.bb,
.cc {
  height: 100%;
}
.cc,
.dd {
  height: 420px;
  overflow: auto;
}
.bookOne {
  height: 100%;
  width: 25%;
}
.img {
  height: 100%;
  width: 100%;
}
.book {
  height: 80px;
  margin: 5px;
  margin-bottom: 15px;
}
.book1 {
  display: -webkit-flex;
  height: 100%;
  display: flex;
  flex-direction: column;
  justify-content: space-between;
  // background-color: #ccc;
  text-align: left;
  font-size: 8px;
}
.bookTwo1 {
  flex: 1;
}
.bookTwo1 h2{
 font-size:16px;
}

.bookTwo2 {
  //     text-overflow: -o-ellipsis-lastline;
  // overflow: hidden;
  // text-overflow: ellipsis;
  // display: -webkit-box;
  // -webkit-line-clamp: 2;
  // -webkit-box-orient: vertical;

  //     text-overflow : ellipsis;
  //     display: -webkit-box;
  // -webkit-line-clamp: 2;
  // -webkit-box-orient: vertical;
  // overflow: hidden;
  display: -webkit-box;
  -webkit-box-orient: vertical;
  -webkit-line-clamp: 2; //文本行数
  overflow: hidden;
  // text-overflow : ellipsis;
  margin-top: 5px;
  margin-bottom: 5px;
  flex: 2;
  font-size: 12px;
}
.bookTwo2 p{
  margin-bottom:0px;
}
.bookTwo3 {
  display: flex;
  justify-content: space-between;
  flex: 1;
}

// .van-tabs {
//     height: 80%;
//     // overflow: auto;
// }
// .van-tabs__wrap  {
//     height: 10%;
// }
// .van-tabs__content {
//     height:calc 80%;
//     overflow: auto;
// }
// .van-tab__pane {
//     height: 100%;
// }
// .van-row {
//     height: 100%;
// }
// .van-col {
//     height: 100%;
//     overflow: auto;
// }
</style>