<template>
  <div class="index">
      <div class="left">
        <v-left :list="friList"></v-left>
      </div>
      <div class="right">
        <v-chat ></v-chat>
      </div>
     <Modal
        v-model="modal1"
        title="输入名字开始聊hi吧"
        @on-ok="ok"
        cancel-text=""
        :closable="false"
        :mask-closable="false">
        <i-input v-model="value" placeholder="请输入您的名字" style="width: 450px"></i-input>
    </Modal>
  </div>
</template>

<script>
import vLeft from "../components/list";
import vChat from "../components/chat";
import Vue from "vue";
import { Modal, Input } from "iview";
Vue.component("Modal", Modal);
Vue.component("iInput", Input);
export default {
  name: "HelloWorld",
  created() {},
  mounted() {
    if (localStorage.getItem("name")) {
      this.modal1 = false;
    }
  },
  methods: {
    ok() {
      console.log(this.value);
      localStorage.setItem("name", this.value);
    },
    cancel() {
      console.log("cancle");
    }
  },
  components: {
    vLeft,
    vChat
  },
  data() {
    return {
      msg: "Welcome to Your Vue.js App",
      modal1: true,
      value: "",
      friList:[]
    };
  }
};
</script>

<style lang="scss" scoped>
.index {
  width: 800px;
  height: 800px;
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
    flex: 1;
    height: 100%;
  }
}
</style>

