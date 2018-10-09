<template>
  <div class="Center clearfix">
    <div class="left">
      <ul>
        <li v-for='(data,key,index) in tabs' :key='data.id'>
          <span @click="tabChange(data.tab, index)" v-bind:class='{on:index==styl}'>{{ data.item }}</span>
        </li>
      </ul>
      <div class="feedback">
        <span>意见反馈</span>
      </div>
    </div>
    <div class="right">
      <div :is="curView"></div>
    </div>
  </div>
</template>

<script>
import Index from '@/components/Index'
import Soft from '@/components/Soft'
import Uidck from '@/components/Uidck'
export default {
  name: 'Center',
  data () {
    return {
      tabs: {
        item: {
          item: '首页',
          tab: 'Index'
        },
        item1: {
          item: '软件入门',
          tab: 'Soft'
        },
        item2: {
          item: '设计教程',
          tab: 'Uidck'
        }
      },
      styl: '0',
      curView: 'Index'
    }
  },
  created: function () {
    var _this = this
    _this.$emit('comHead', true)
  },
  components: {
    Index,
    Soft,
    Uidck
  },
  methods: {
    tabChange (tabItem, num) {
      this.styl = num
      this.curView = tabItem
    }
  }
}
</script>

<style>
  .Center{ min-height: 100%; height: 100%;}
  .left{ position: fixed; left: 0; top: 80px; width: 120px; height: calc(100% - 80px); background-color: #666;}
  .left ul{ margin-top: 20px;}
  .left ul li{ margin-bottom: 20px;}
  .left ul li span{ display: block; width: 90px; height: 35px; line-height: 35px; margin: 0 auto; text-align: center; cursor: pointer;}
  .left ul li span.on{ background-color: bisque; border-radius: 5px;}
  .feedback{ position: absolute; bottom: 30px; left: 15px; width: 90px; line-height: 40px; border-top: 1px solid #fff; text-align: center;}
  .feedback span{ color: #fff; cursor: pointer;}
  .right{ margin-left: 120px; padding: 80px 20px 30px; background-color: #333;}
</style>
