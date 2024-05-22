<script>
import { ref } from 'vue';
export default {
  data() {
    return {
      username: '',
      message: '',
      messages: []
    };
  },
  methods: {
    submitMessage() {
      if (!this.message) {
        alert('请输入内容');
        return;
      }
      if (!this.username) {
        this.username = '匿名';
      }
      // 创建新消息对象并添加到 messages 数组
      const newMessage = {
        id: Date.now(), // 使用时间戳作为唯一标识
        username: this.username,
        message: this.message,
        time: this.getCurrentTime()
      };
      this.messages.unshift(newMessage); // 添加到数组开头
      this.username = '';
      this.message = '';
    },
    getCurrentTime() {
      const now = new Date();
      const year = now.getFullYear();
      const month = ('0' + (now.getMonth() + 1)).slice(-2);
      const day = ('0' + now.getDate()).slice(-2);
      const hours = ('0' + now.getHours()).slice(-2);
      const minutes = ('0' + now.getMinutes()).slice(-2);
      const seconds = ('0' + now.getSeconds()).slice(-2);
      return `${year}/${month}/${day} ${hours}:${minutes}:${seconds}`;
    }
  }
};
</script>
<template>
    <div class="messages">
      <h1>
        留言板
      </h1>
      <div class="form">
        <input v-model="username" placeholder="用户名">
        <textarea v-model="message" placeholder="留言内容"></textarea>
        <button id="SubmitBtn" @click="submitMessage()">留言</button>
      </div>
      <div id="messageBoard">
        <!-- <div v-for="msg in messages" :key="msg.id" class="message"></div> -->
        <div class="message">
          <div class="class-info">
            <div class="info">
              <img src="./components/img/1.jpg" alt="" width="50px" height="50px">
              <strong>咔叽）</strong>
            </div>
            <span>发布于:2024/5/12 20:47:23</span>
          </div>
          <div class="content">你好</div>
        </div>
      </div>
      <div id="messageBoard">
      <!-- 使用 v-for 循环渲染消息 -->
      <div v-for="msg in messages" :key="msg.id" class="message">
        <div class="class-info">
          <div class="info">
            <img src="./components/img/1.jpg">
            <strong>{{ msg.username }}</strong>
          </div>
          <span>发布于：{{ msg.time }}</span>
        </div>
        <div class="content">{{ msg.message }}</div>
      </div>
    </div>
    </div>
</template>
<style scoped>
.messages{
  margin:100px;
  width: 1200px;
  padding: 50px 100px;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  background-color: rgba(255,255,255,0.43);
  box-shadow: 0 19px 30px #00000020;
  border-radius: 20px;
}
.form{
  display: flex;
  justify-content: center;
  /* align-items: center; */
  position: relative;
  flex-direction: column;
  width: 100%;
  padding-bottom: 70px;
}
input:focus,
textarea:focus{
  outline: none;
}
input,
textarea{
  border: none;
  color: #000;
  margin-bottom: 40px;
  font: 900 40px '';
  border-radius: 10px;
  padding: 30px;
}
.messages h1{
  width: 100%;
  text-align: left;
  margin-bottom: 70px;
  font-size: 140px;
  background-image: linear-gradient(135deg,#667eea 0%,#764ba2 100%);
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
  letter-spacing: 10px;
}
#SubmitBtn{
  position: absolute;
  right: 0;
  bottom: 0;
  background-image: linear-gradient(90deg,#e0c3fc 0%,#8ec5fc 100%);
  border: 0;
  font-size: 30px;
  width: 200px;
  height: 70px;
  border-radius: 50px;
}
#messageBoard{
  width: 100%;
  text-align: left;
}
@keyframes messageFadeIn{
  to{
    opacity: 1;
  }
}
.message{
  width: 100%;
  margin:10px;
  padding: 10px;
  opacity: 0;
  animation: messageFadeIn 0.5s ease forwards;
  background-image: linear-gradient(90deg,#8ec5fc 0%,#e0c3fc 100%);
  background-color: #fff;
  margin:70px 0;
  border-radius: 10px;
  box-shadow: 0 10px 20px #00000026;
  text-shadow: 0 0 20px #ffffff;
}
.class-info{
  display: flex;
  height: 100px;
  justify-content: space-between;
  align-items: center;
  font-size: 36px;
  position: relative;
}
.info{
  transform: translateY(-30px);
}
.info img{
  width: 150px;
  height: 150px;
  border-radius: 50%;
  border: 10px #fff solid;
}
strong{
  position: absolute;
  width: 800px;
  letter-spacing: 3px;
  top:70px;
  left: 170px;
}
.class-info span{
  position: absolute;
  top:10px;
  right: 10px;
}
.content{
  font-size: 36px;
  margin: 30px;
  width: 95%;
}
</style>