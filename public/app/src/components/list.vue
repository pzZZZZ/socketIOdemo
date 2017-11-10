<template>
  <div class="list">
        <div class="listheader" @click="hideMenu">
            在线列表
        </div>
        <transition  
        name="custom-classes-transition"
    enter-active-class="animated bounceInDown"
    leave-active-class="animated hinge">
        <div class="chatList" v-show="menuShow">
            <ul>
                
                <li v-for="(item,i) in list"  @click="changeIndex(i)">
                    <div v-if="i==index" class="act item">    {{item}}{{i}}</div>
                    <div v-else class="item">    {{item}}{{i}}</div>
                </li>

            </ul>
        </div>
         </transition>
  </div>
</template>
<script>
export default {
  data() {
    return {
      list: ["张三", "李四", "张三", "李四", "张三", "李四", "张三", "李四"],
      index: 0,
      menuShow: true
    };
  },
  methods: {
    changeIndex(i) {
      this.index = i;
    },
    hideMenu() {
      this.menuShow = !this.menuShow;
    }
  }
};
</script>
<style lang="scss" scoped>
.listheader {
  text-align: center;
  font-size: 16px;
  background: #3399ff;
  color: #fff;
  padding: 10px 0;
  cursor: pointer;
}
.chatList {
  ul {
    li {
      .item {
        cursor: pointer;
        padding: 10px 0;
        text-align: center;
        background: #eee;
        font-size: 14px;
        &:hover {
          background: #5cadff;
          color: #fff;
          transition: 0.4s;
        }
      }
      .act {
        background: #5cadff;
        color: #fff;
      }
    }
  }
}

</style>


