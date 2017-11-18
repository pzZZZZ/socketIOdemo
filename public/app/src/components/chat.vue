<template>
  <div class="chat" @keyup.enter="Csend">
    <div class="chat-header">聊天窗口</div>
    <div class="chat-list">
      <div class="list wrapper" >
        <ul>
          <li v-for="(item,i) in chat">
            <div class="system" v-html="item.msg" v-if="item.type==1">
              
            </div>
            <div class="user" v-html="item.msg" v-if="item.type==2">
              
            </div>

          </li>
        </ul>
      </div>
    </div>
    <quill-editor v-model="content" ref="myQuillEditor" :options="editorOption" @blur="onEditorBlur($event)" @focus="onEditorFocus($event)"
      @ready="onEditorReady($event)">
    </quill-editor>
    <div class="btns">
      
       <Button @click="Csend" >发送</Button>
    </div>
  </div>
</template>
<script>
import Vue from "vue";
import Bscroll from "better-scroll";
import VueQuillEditor from "vue-quill-editor";
import { Button } from "iview";
Vue.component("Button", Button);
import VueSocketio from "vue-socket.io";
Vue.use(VueSocketio, "http://45.32.181.136:3000");
Vue.use(VueQuillEditor);
export default {
  components: {},
  data() {
    return {
      chat: [],
      content: "",
      editorOption: {
        // some quill options
      }
    };
  },
  mounted() {
    this.name = localStorage.getItem("name");
    const wrapper = document.querySelector(".wrapper");
    this.scroll = new Bscroll(wrapper, {
      scrollbar: true
    });

    this.scroll.on("refresh", () => {
      this.scroll.scrollTo(0, this.scroll.maxScrollY, "swing");
    });
    // this.scroll.on("scroll", () => {
    //   console.log(123);
    // });

    this.socketarea();
    this.Cacc();
    this.isonline();
  },
  sockets: {
    // connect: function() {
    //   this.id = this.$socket.id;
    // },
    // customEmit: function(val) {
    //   console.log(
    //     'this method was fired by the socket server. eg: io.emit("customEmit", data)'
    //   );
    // }
  },
  computed: {
    editor() {
      return this.$refs.myQuillEditor.quill;
    }
  },
  methods: {
    onEditorBlur(editor) {
      console.log("editor blur!", editor);
    },
    onEditorFocus(editor) {
      console.log("editor focus!", editor);
    },
    onEditorReady(editor) {
      console.log("editor ready!", editor);
    },
    onEditorChange({ editor, html, text }) {
      console.log("editor change!", editor, html, text);
      this.content = html;
    },
    socketarea() {
      this.$socket.emit("event", { name: this.name });
      this.$options.sockets.system = data => {
        console.log(data);
        // this.chat.push(`系统说：${data}`);
        this.chat.push({
          type: 1,
          msg: `系统说：${data}`
        });
        this.scroll.refresh();
      };
    },
    isonline() {
      // this.$options.sockets.isonline = data => {
      //   this.$socket.emit("onlinelist", { name: this.name });
      // };
    },
    Csend() {
      this.$socket.emit("Csend", { name: this.name, msg: this.content });
      this.content = "";
    },
    Cacc() {
      this.$options.sockets.Ssend = data => {
        console.log(data);
        this.$parent.friList = data.friLisht;
        let str = `${data.name}：${data.msg}`;
        this.chat.push({
          type: 2,
          msg: str
        });

        setTimeout(() => {
          this.scroll.refresh();
          console.log(this.scroll);
        });
      };
    }
  }
};
</script>
<style lang="scss">
.user {
  font-size: 14px;
  color: #000;
  text-indent: 2em;
  padding: 10px 0;
  display: flex;
  p {
    text-indent: 0;
    img {
      width: 200px;
    }
  }
}
.btns {
  display: flex;
  justify-content: flex-end;
  button {
    margin-top: 20px;
    margin-right: 30px;
  }
}
.ql-snow {
  background: #fff;
}
.ql-container {
  height: 150px;
  overflow-y: scroll;
}
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
.system {
  color: red;
  font-size: 18px;
  display: flex;
}
</style>