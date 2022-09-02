<script setup>
import { ref } from "vue";

defineProps({
  msg: String,
});

const isHome = ref(true);
const isIn = ref(false);
const queryString = window.location.search;
const urlParams = new URLSearchParams(queryString);
const name = urlParams.get("n");
const gender = urlParams.get("g");
const id = urlParams.get("i");
const avatar = "/avatar/" + urlParams.get("a") + ".jpg";
var today = new Date();
const scanTime = today.getFullYear() + "-" + (today.getMonth() + 1) + "-" + today.getDate() + " " + today.getHours() + ":" + today.getMinutes() + ":" + today.getSeconds();
</script>

<template>
  <div class="main passMain" v-if="isHome">
    <!-- 通行码页面 -->
    <img class="pass-code" src="/imgs/passCode.jpg" />
    <div class="pass-text pass-name">{{ name }}</div>
    <div class="pass-text pass-id">{{ id }}</div>
    <div class="pass-dateTime">{{ scanTime }}</div>
    <button class="enter-button" type="button" @click="isHome = !isHome">打开出入校通行卡</button>
  </div>
  <div class="main enterMain" v-else="isHome">
    <!-- 出入校码页面 -->
    <img class="enter-code" src="/imgs/enterCode.jpg" />
    <img class="enter-state" src="/imgs/in.jpg" v-if="isIn" />
    <img class="enter-state" src="/imgs/out.jpg" v-else="isIn" />
    <button class="state-button" type="button" @click="isIn = !isIn"></button>
    <img class="enter-img" src="/imgs/out_text.jpg" v-if="isIn" />
    <img class="enter-avatar" :src="avatar" />
    <div class="enter-dateTime">{{ dateTime }}</div>
    <div class="enter-text enter-name">{{ name }}</div>
    <div class="enter-text enter-gender">{{ gender }}</div>
    <div class="enter-text enter-id">{{ id }}</div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      dateTime: "",
    };
  },
  methods: {
    dateTimeTicker: function () {
      var self = this;
      setInterval(function () {
        var today = new Date();
        var date = today.getFullYear() + "年" + (today.getMonth() + 1) + "月" + today.getDate() + "日";
        var time = today.getHours() + ":" + today.getMinutes() + ":" + today.getSeconds();
        var dateTime = date + " " + time;
        self.dateTime = dateTime;
      }, 1000);
    },
  },
  mounted() {
    this.dateTimeTicker();
  },
};
</script>

<style>
.main {
  height: 100%;
  width: 100%;
}
.passMain {
  background: #f2f2f2;
}
.pass-code {
  width: 100%;
}
.pass-dateTime {
  position: absolute;
  left: 39vw;
  top: 48.5vw;
  font-size: 4.5vw;
  color: transparent;
  text-shadow: 0 0 0.8px #194280;
}
.pass-text {
  position: absolute;
  top: 17vw;
  font-size: 3.2vw;
  color: transparent;
  text-shadow: 0 0 0.8px #ffffff;
  font-weight: bold;
}
.pass-name {
  left: 14.4vw;
}
.pass-id {
  left: 60vw;
}
.enter-button {
  position: absolute;
  top: 135vw;
  left: 10vw;
  color: #00000000;
  background: #00000000;
}
button:focus {
  outline: none;
}
button:hover {
  border: none;
}
.enterMain {
  background: #60ce6d;
}
.enter-text {
  position: absolute;
  left: 45.2vw;
  font-size: 3.1vw;
  color: transparent;
  text-shadow: 0 0 0.8px #444;
}
.enter-name {
  bottom: 65.3vw;
}
.enter-gender {
  bottom: 59.7vw;
}
.enter-id {
  bottom: 54.5vw;
}
.enter-code {
  width: 100%;
  position: absolute;
  left: 0;
  bottom: 0;
}
.enter-state {
  position: absolute;
  width: 40vw;
  left: 50vw;
  transform: translateX(-50%);
  bottom: 162vw;
}
.enter-img {
  position: absolute;
  width: 22.2vw;
  left: 49.8vw;
  transform: translateX(-50%);
  bottom: 146.5vw;
}
.state-button {
  position: absolute;
  left: 50vw;
  transform: translateX(-50%);
  bottom: 162vw;
  width: 40vw;
  height: 10vw;
  color: #00000000;
  background: #00000000;
}
.enter-avatar {
  position: absolute;
  width: 33.5vw;
  bottom: 81.5vw;
  left: 50vw;
  transform: translateX(-50%);
}
.enter-dateTime {
  position: absolute;
  left: 50vw;
  bottom: 137vw;
  font-size: 4vw;
  transform: translateX(-50%);
  color: #67ba67;
}
</style>
