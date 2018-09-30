<template>
  <div class="Uidck">
    <div class='nav' v-for='(data, index) in category' :key="data.id">
      <div>
        {{data.name}}
      </div>
      <ul>
        <li v-for='(data1, key) in data.items'>
          <span :class="{'active':data1.active}" :key='data1.id'>{{data1.name}}</span>
        </li>
      </ul>
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
    axios.get('/static/json/uiDckTab.json')
      .then(function (response) {
        var _this = this
        _this.category = response.data.category
      }).catch(function (error) {
        console.log(error)
      })
  },
  components: {
  },
  methods: {
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
    padding: 60px 0;
    background-color: burlywood;
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
