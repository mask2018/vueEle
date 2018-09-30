<template>
  <div class="Uidck">
    <div class='nav' v-for='(items,index) in category'>
      <div class='mutil-query-title' v-if='items.name' :key="items.id">
        {{items.name}}
        <span style='margin-left: 20px;' @click='allIn(index)'>全选</span>
      </div>
      <ol v-if='items.items.length'>
        <li v-for='(item,key) in items.items'>
          <span :class="{'active':item.active}" @click='handle(index,key)' :key='item.id'>{{item.name}}</span>
        </li>
      </ol>
    </div>
    <div class="uiDckList">
      <ul>
        <li v-for="data in uiDckListLi">
          <div class="uiDckListAll">
            <a :href="data.method" class="uiDckListImg"><img v-bind:src="data.src"/></a>
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
      count: 0
    }
  },
  created () {
    axios.get('/static/json/uiDckTab.json')
      .then(function (response) {
        console.log(response.data)
        var _this = this
        _this.items.items = response.data.category
      }).catch(function (error) {
        console.log(error)
      })
  },
  components: {
  },
  methods: {
    handle: function (index, key) {
      var item = this.category[index].items
      item.filter(function (v, i) {
        if (i === key) {
          v.active = true
          this.list.condition.filter(function (v2, i) {
            if (v.name === v2.name) {
              this.list.condition.splice(i, 1)
            }
          })
        }
      })
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
            display: block; width: 100%; height: 150px;
            img{ width: 100%; height: 100%; border-radius: 6px 6px 0 0;}
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
    }
  }
}
</style>
