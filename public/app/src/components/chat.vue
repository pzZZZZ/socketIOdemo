<template>
  <div class="chat">
    <div class="chat-header">聊天窗口</div>
    <div class="chat-list">
      <div class="list wrapper">
        <ul>
          <li v-for="(item,i) in chat">
            <div class="system" v-html="item">
              
            </div>

          </li>
        </ul>
      </div>
    </div>
    <quill-editor v-model="content" ref="myQuillEditor" :options="editorOption" @blur="onEditorBlur($event)" @focus="onEditorFocus($event)"
      @ready="onEditorReady($event)">
    </quill-editor>
    <div class="btns">
      
       <Button @click="Csend">发送</Button>
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
Vue.use(VueSocketio, "http://localhost:3000");
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
    const wrapper = document.querySelector(".wrapper");
     this.scroll = new Bscroll(wrapper, {
      scrollbar: true
    });
    this.socketarea();
  },
  sockets: {
    connect: function() {
      this.id = this.$socket.id;
    },
    customEmit: function(val) {
      console.log(
        'this method was fired by the socket server. eg: io.emit("customEmit", data)'
      );
    }
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
      this.$socket.emit("event", { name: "pzzz" });

      this.$options.sockets.system = data => {
        console.log(data);
        this.chat.push(`系统说：${data}`)
        this.scroll.refresh()
        
      };
    },
    Csend(){
      this.$socket.emit("Csend", {name:'pzzz',msg:this.content});
       this.$options.sockets.Ssend = data => {
        console.log(data);
        this.chat.push(`${data.name}：${data.msg}`)
        this.scroll.refresh()
        
      };
    }
  }
};
</script>
<style lang="scss">
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
</style>