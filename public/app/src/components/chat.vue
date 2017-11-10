<template>
  <div class="chat">
      <div class="chat-header">聊天窗口</div>
      <div class="chat-list">
          <div class="list wrapper" >
              <ul>
                  <li v-for="(item,i) in chat">
                      <div class="system">
                          {{item}}
                      </div>
                      
                      </li>
              </ul>
          </div>
      </div>
  </div>
</template>
<script>
import Bscroll from "better-scroll";
import socket from "socket.io/lib/socket.js";
export default {
  data() {
    return {
      chat: [1, 2, 23, 123, 12412, 412412, 412, 412412]
    };
  },
  mounted() {
    const wrapper = document.querySelector(".wrapper");
    const scroll = new Bscroll(wrapper, {
      scrollbar: true
    });
    this.Login();
  },
  methods: {
    Login() {
      socket.emit("event", { name: "pzzz" });
    }
  }
};
</script>
<style lang="scss" scoped>
.chat {
  width: 100%;
  background: #3399ff;
  height: 100%;
}
.chat-header {
  height: 44px;
  background: #3399ff;
  line-height: 44px;
  font-size: 24px;
  text-align: center;
}
.chat-list {
  height: 450px;
  padding: 20px;
  .wrapper {
    position: relative;
  }
  .list {
    background: #fff;
    height: 100%;
    overflow: hidden;
    ul {
      li {
        .system {
          font-size: 42px;
        }
      }
    }
  }
}
</style>


