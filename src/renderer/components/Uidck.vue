<template>
  <div class="Uidck">
    <div class="nav">
      <div class="navCen" v-for='(data, index) in category' :key="data.id">
        <span class="navTitle">
          {{data.name}}
        </span>
        <ul class="navList">
          <li v-for="(data1, key) in data.items" @click="navLab(index, key)"  :class="{'on':data1.active}" :key='data1.id'>
            {{data1.name}}
          </li>
        </ul>
      </div>
    </div>
    <div class="uiDckList">
      <ul>
        <li v-for="data in uiDckListLi">
          <div class="uiDckListAll">
            <a :href="data.method" class="uiDckListImg">
              <img v-bind:src="data.src"/>
              <span>{{data.time}}</span>
            </a>
            <a :href="data.method" class="uiDckListTitle">{{data.title}}</a>
            <p class="uiDckListDetail">
              <span class="fl">初学者</span>
              <span class="fr">333万人已学</span>
            </p>
          </div>
        </li>
      </ul>
    </div>
  </div>
</template>

<script>
import axios from 'axios'
export default {
  name: 'Uidck',
  data () {
    return {
      uiDckListLi: [],
      page: 1,
      category: [],
      sel: []
    }
  },
  created () {
    var _this = this
    axios.get('/static/json/uiDckTab.json')
      .then(function (response) {
        _this.category = response.data.category
      }).catch(function (error) {
        console.log(error)
      })
  },
  components: {
  },
  methods: {
    navLab: function (index, key) {
      var item = this.category[index].items
      item.filter(function (v, i) {
        if (i === key) {
          v.active = true
        } else {
          v.active = false
        }
      })
    },
    select: function (index, i, j) {
      var _this = this
      _this.sel[i] = j
      _this.$set(_this.sel, i, j)
    },
    getPage (page) {
      var _this = this
      axios.get('/static/json/uiDckList.json', {
        params: {
          page: page,
          limit: 1
        }
      })
        .then(function (response) {
          _this.uiDckListLi = response.data.uiDckListLi
        }).catch(function (error) {
          console.log(error)
        })
    }
  },
  mounted () {
    this.getPage(this.page)
    this.select(this.index, this.ind)
  }
}
</script>

<style lang="less" scoped>
.Uidck{
  margin-left: 30px;
  margin-right: 30px;
  padding: 30px 0;
  .nav{
    margin-bottom: 20px;
    padding-top: 20px;
    background-color: burlywood;
    .navCen{
      position: relative;
      padding-bottom: 20px;
      .navTitle{
        position: absolute;
        left: 0;
        top: 0;
        display: block;
        width: 100px;
        padding: 3px 0;
        text-align: center;
        border: 1px solid burlywood;
      }
      .navList{
        margin-left: 100px;
        overflow: hidden;
        li{
          float: left;
          padding: 3px 10px;
          border: 1px solid burlywood;
          border-radius: 30px;
          cursor: pointer;
        }
        li.on{
          border: 1px solid #fff;
        }
      }
    }
  }
  .uiDckList{
    ul{
      overflow: hidden;
      li{
        float: left;
        width: 215px; margin-right: 65px; margin-bottom: 30px;
        background-color: #ddd; border-radius: 6px;
        .uiDckListAll{
          .uiDckListImg{
            position: relative; display: block; width: 100%; height: 150px;
            img{ width: 100%; height: 100%; border-radius: 6px 6px 0 0;}
            span{
              position: absolute; right: 10px; bottom: 10px; padding: 3px 10px; background-color: rgba(0,0,0,.5); color: #fff; border-radius: 6px;
            }
          }
          .uiDckListTitle{
            display: block; width: 90%; margin: 16px auto 0;
            white-space: nowrap; overflow: hidden; text-overflow: ellipsis;
          }
          .uiDckListDetail{
            width: 90%; margin: 0 auto; padding: 16px 0; overflow: hidden;
          }
        }
      }
      li:nth-of-type(6n){
        margin-right: 0;
      }
    }
  }
}
</style>
