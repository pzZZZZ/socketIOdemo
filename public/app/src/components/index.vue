<template>
  <div class="index">
      <div class="left">
        <v-left></v-left>
      </div>
      <div class="right">
        <v-chat></v-chat>
      </div>
  </div>
</template>

<script>
import vLeft from "../components/list";
import vChat from "../components/chat";
export default {
  name: "HelloWorld",
  components: {
    vLeft,
    vChat
  },
  data() {
    return {
      msg: "Welcome to Your Vue.js App"
    };
  }
};
</script>

<style lang="scss" scoped>
.index {
  width: 800px;
  height: 600px;
  background: #ffcc99;
  margin: 0 auto;
  margin-top: 100px;
  border-radius: 10px;
  overflow: hidden;
  display: flex;
  .left {
    width: 200px;
    height: 100%;
    // background: #ffcccc;
  }
  .right {
    flex:1;
    height: 100%;
    
  }
}
</style>

