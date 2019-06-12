<template>
  <div>
    <div id="app">
      <BasicModal ref="counting" headerMsg="HELLO" paragraghMsg="hello world" a="10"/>
      <button @click="openCountDown">CountDown</button>
    </div>
  </div>
</template>

<script>
import HelloWorld from "./components/HelloWorld.vue";
import BasicModal from "@/components/BasicModal.vue";

export default {
  name: "app",
  components: {
    // HelloWorld
    BasicModal
  },
  data() {
    return {
      isCountDownVisible: false,
      num: 15
    };
  },
  methods: {
    success() {
      this.$refs.counting.status = "success";
      this.$refs.counting.headerMsg = "SUCCESS";
      this.$refs.counting.paragraghMsg = "success";
    },
    fail() {
      this.$refs.counting.status = "failure";
      this.$refs.counting.headerMsg = "FAILURE";
      this.$refs.counting.paragraghMsg = "failure";
    },
    startCount() {
      this.$refs.counting.open(this.alert);
    },
    openCountDown() {
      this.isCountDownVisible = true;
      this.startCount();
    },
    closeCountDown() {
      this.$refs.counting.close();
    },

    alert() {
      alert("hello");
    }
  }
};
</script>

<style>
#app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
