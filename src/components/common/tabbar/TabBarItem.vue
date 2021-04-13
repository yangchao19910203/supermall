<template>
  <div class="tab-bar-item" @click="itemClick">
    <div v-if="!isActive"><slot name="item-icon"></slot></div>
    <div v-else><slot name="item-icon-active"></slot></div>
    <div :style="activeStyle"><slot name="item-text"></slot></div>
    <!--<div :class="{active: isActive}"><slot name="item-text"></slot></div>-->
    <!--所有的item都展示同一个图片，同一个文字-->
    <!--<img src="../../assets/img/tabbar/home.svg" alt="">
    <div>首页</div>-->
  </div>
</template>

<script>
    export default {
      name: "TabBarItem",
      props: {
        path: String,
        activeColor: {
          type: String,
          default: 'red'
        }
      },
      data(){
        return {
          //isActive: true
        }
      },
      computed: {
        isActive(){
          // this.$route.path: 表示的是当前活跃的路由里的path路径
          return this.$route.path.indexOf(this.path) !== -1   // 判断当前活跃的路由的path和我们的传入的path是否一致
        },
        activeStyle(){
          return this.isActive ? {color: this.activeColor} : {}
        }
      },
      methods: {
          itemClick(){
            //console.log("itemClick");
            this.$router.replace(this.path)
          }
      }
    }
</script>

<style scoped>
  /*水平布局进行平分页面*/
  .tab-bar-item {
    flex: 1;
    text-align: center;
    height: 49px;
    font-size: 14px;
  }

  .tab-bar-item img {
    width: 24px;
    height: 24px;
    margin-top: 3px;
    vertical-align: middle;
    margin-bottom: 2px;
  }

  .active {
    color: red;
  }
</style>
