<template>
  <div class="Soft">
    <ul class="softTab">
      <li v-for="(data, index) in softTabList" @click="softTab(index)" v-bind:class="{'on': index == style}" :key="data.id"><a href="javascript:;">{{data.name}}</a></li>
    </ul>
    <div class="softList">
      <ul>
        <li v-for="data in softListLi">
          <div class="softListAll">
            <a :href="data.method" class="softListImg"><img v-bind:src="data.src"/></a>
            <div class="softListCen">
              <p class="softListTitle">
                <a :href="data.method">
                  {{data.title}}
                  <i v-if="data.label" v-bind:class="[data.label == 'hot' ? 'hotStyle' : 'newStyle']">{{data.label}}</i>
                </a>
                <span v-bind:class="[data.state == '已完结' ? 'endStyle' : 'ufdStyle']">{{data.state}}</span>
              </p>
              <p class="softListDetail">
                <span>学习人数 888，000</span>
                <span>主课程数 32节</span>
                <span>练习题目 22节</span>
              </p>
            </div>
          </div>
        </li>
      </ul>
    </div>
  </div>
</template>

<script>
import axios from 'axios'
export default {
  name: 'Soft',
  data () {
    return {
      softTabList: [
        {name: '全部'},
        {name: '平面设计软件'},
        {name: 'UI设计软件'},
        {name: '环艺建筑软件'},
        {name: '影视动画软件'},
        {name: '游戏制作软件'},
        {name: '工业产品软件'}
      ],
      style: 0,
      softListLi: [],
      page: 1
    }
  },
  created () {
  },
  components: {
  },
  methods: {
    softTab: function (index) {
      this.style = index
    },
    getPage (page) {
      var _this = this
      axios.get('/static/json/sofeListLi.json', {
        params: {
          page: page,
          limit: 1
        }
      })
        .then(function (response) {
          _this.softListLi = response.data.softListLi
        }).catch(function (error) {
          console.log(error)
        })
    }
  },
  mounted () {
    this.getPage(this.page)
  }
}
</script>

<style lang="less">
.Soft{
  margin-left: 30px;
  margin-right: 30px;
  padding: 30px 0;
  .softTab{
    display: flex;
    background-color: #666;
    li{
      flex: 1;
      line-height: 70px;
      font-size: 18px;
      text-align: center;
      a{ display: inline-block; color: #fff;}
    }
    li.on{
      a{ color: chocolate; border-bottom: 5px solid #f00;}
    }
  }
  .softList{
    ul{
      overflow: hidden;
      li{
        margin-top: 20px; float: left; width: 49%;
        background-color: #666; color: #fff;
        .softListAll{
          position: relative;
          padding: 20px; overflow: hidden;
          .softListImg{
            float: left; width: 96px; height: 96px;
            img{ width: 96px; height: 96px;}
          }
          .softListCen{
            margin-left: 120px;
            .softListTitle{
               line-height: 36px; margin: 10px 0 15px; font-size: 18px;
              a{
                position: relative; color: #fff;
                i{
                  position: absolute; right: -40px; top: -20px; line-height: 23px; padding: 0 8px;
                  font-size: 12px; border-radius: 20px;
                }
                .hotStyle{ background-color: red;}
                .newStyle{ background-color: cornflowerblue}
              }
              span{
                 margin-left: 50px; padding: 0 10px; line-height: 30px; border: 1px solid #ddd; border-radius: 30px; font-size: 14px;
              }
              .endStyle{ background-color: #666; color: burlywood;}
              .ufdStyle{ background-color: #ddd; color: #333;}
            }
            .softListDetail{}
          }
        }
      }
      li:nth-of-type(even){
        float: right;
      }
    }
  }
}
</style>
