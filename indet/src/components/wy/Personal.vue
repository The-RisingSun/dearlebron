<template>
  <div id="personal">
    <Headnav></Headnav>
    <Headsearch class="headsearch-border"></Headsearch>
    <div class="box">
      <div class="box-left">
        <el-col class="show" :span="120" >
          <h5>大麦</h5>
          <el-menu
                  default-active=inde
                  class="el-menu-vertical-demo"
                  @open="handleOpen"
                  @close="handleClose"
                  background-color="#fff"
                  text-color="#495060"
                  active-text-color="#ff3c1b">
            <el-submenu index="1">
              <template slot="title">交易中心</template>
              <el-menu-item @click="PersonOrder(order, 1)" :class="index === 1 ? active : false" to="/" index="1">{{order}}</el-menu-item>
            </el-submenu>
            <el-submenu index="2">
              <template slot="title">账户中心</template>
              <el-menu-item to="/Personal/PersonInfo" @click="PersonInfo(account, 2)" :class="index === 2 ? active : false" index="2" >个人信息</el-menu-item>
              <el-menu-item  @click="PersonTicket(contact, 3)" :class="index === 3 ? active : false" index="3">常用购票人</el-menu-item>
            </el-submenu>
          </el-menu>
        </el-col>
        <div  class="box-right">
          <router-view ref="mychild"/>
        </div>
      </div>
    </div>
    <Footer></Footer>
  </div>
</template>

<script>
import Headnav from '../ljd/Headnav'
import Headsearch from '../ljd/Headsearch'
import Footer from '../ljd/Footer'
import { mapMutations } from 'vuex'
export default {
  name: 'Personal',
  data () {
    return {
      order: '订单管理',
      account: '个人信息',
      contact: '常用购票人',
      index: 1,
      active: 'active'
    }
  },
  watch: {
    $route (to, from) {
      console.log(to.path === '/personal/PersonInfo/2')
      if (to.path === '/personal/PersonInfo/2') {
        console.log(222)
        this.index = 2
      } else if (to.path === '/personal/PersonTicket/3') {
        this.index = 3
      } else {
        this.index = 1
      }
      console.log(from.path)
    }
  },
  components: {
    Headnav,
    Headsearch,
    Footer
  },
  methods: {
    ...mapMutations(['setScroll']),
    handleOpen (key, keyPath) {
      console.log(key, keyPath)
    },
    handleClose (key, keyPath) {
      console.log(key, keyPath)
    },
    PersonInfo (cen, i) {
      this.index = i
      this.setScroll(cen)
      this.$router.push({path: '/Personal/PersonInfo', name: 'PersonInfo'})
    },
    PersonOrder (cen, i) {
      this.index = i
      this.setScroll(cen)
      this.$router.push({path: '/Personal/'})
    },
    PersonTicket (cen, i) {
      this.index = i
      this.setScroll(cen)
      this.$router.push({path: '/Personal/PersonTicket', name: 'PersonTicket'})
    }
  }
}
</script>

<style scoped lang="less">
#personal{
  background: #f5f5f5;
  .headsearch-border{
    border-bottom: 2px solid red;
  }
  .box{
    width: 1200px;
    -height: 374px;
    margin: 20px auto;
    background: #fff;
    overflow: hidden;
    .box-left{
      width: 200px;
      // height: 100%;
      -box-sizing: border-box;
      .el-menu-vertical-demo{
        border: none;
        box-shadow: 0 2px 2px rgba(10,16,20,.24),0 0 2px rgba(10,16,20,.12);
      }
      .active{
        border-right: 1px solid red
      }
      h5{
        width: 200px;
        height: 50px;
        line-height: 50px;
        background: #ff5c41;
        text-indent: 22px;
        font-size: 14px;
        color: #fff;
        font-weight: normal;
      }
      .el-submenu__title{
        width: 200px;
      }
    }
    .box-right{
      padding-left: 220px;
      width: 980px;
    }
  }
}
</style>
