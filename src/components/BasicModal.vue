<template>
  <div v-show="showModal">
    <transition name="modal">
      <div>
        <div class="overlay">
          <div class="modal">
            <div class="col-12">
              <Success v-show="isSuccess"/>
              <Fail v-show="isFail"/>
              <Progess v-show="!isDone" min="0" max="100" :value="value" :text="time"/>
            </div>
            <h3>{{hMsg}}</h3>
            <p>{{pMsg}}</p>
            <button v-show="isFail" @click="close">Close</button>
          </div>
        </div>
      </div>
    </transition>
    <!-- <button @click="isOpen = !isOpen;">{{ isOpen ? "Close" : "Open" }} modal</button> -->
  </div>
</template>

<script>
import Progess from "@/components/ProgressCircle.vue";
import Success from "@/components/Success.vue";
import Fail from "@/components/Fail.vue";
export default {
  name: "basic-modal",
  props: ["headerMsg", "paragraghMsg", "a", "text"],
  components: {
    Progess,
    Fail,
    Success
  },
  data: function() {
    return {
      headerMsg: "",
      paragraghMsg: "",
      showModal: false,
      isDone: false,
      isSuccess: false,
      isFail: false,
      isOpen: false,
      date: 0,
      value: 0,
      totalSeconds: 0,
      actualSeconds: 0,
      a: 0,
      status: "failure"
    };
  },
  mounted() {},
  methods: {
    reset() {
      this.actualSeconds = 0;
      this.isDone = false;
      this.isFail = false;
      this.isOpen = false;
      this.isSuccess = false;
      this.value = 0;
      //   this.date = this.a;
      //   this.totalSeconds = this.a;
    },
    open(status, method) {
      this.showModal = true;
      this.count(status, method);
    },
    close() {
      this.showModal = false;
      this.reset();
    },
    count(method) {
      this.status = "failure";
      this.totalSeconds = this.a;
      this.date = this.a;

      setInterval(() => {
        if (this.value === 90) {
          if (this.status == "success") {
            this.isDone = true;
            this.isSuccess = true;
            setTimeout(() => this.close, 1500);
          } else if (this.status == "failure") {
            this.headerMsg = "FAILURE";
            this.isDone = true;
            this.isFail = true;
          }
          // here you can call your method after the count down
          // setTimeout(() => method(), 1000);
        }
        if (this.date >= 1) {
          this.date = this.date - 1;
          this.actualSeconds++;
          this.value = (this.actualSeconds * 100) / this.totalSeconds;

          console.log(this.value);
        } else {
        }
      }, 1000);
    }
  },

  computed: {
    time: function() {
      return this.date;
    },
    hMsg: function() {
      return this.headerMsg;
    },
    pMsg: function() {
      return this.paragraghMsg;
    }
  }
};
</script>

<style scoped>
.svg {
}
.modal {
  width: 500px;
  margin: 0px auto;
  padding: 20px;
  background-color: #fff;
  border-radius: 2px;
  box-shadow: 0 2px 8px 3px;
  transition: all 0.2s ease-in;
  font-family: Courier;
}
.fadeIn-enter {
  opacity: 0;
}

.fadeIn-leave-active {
  opacity: 0;
  transition: all 0.2s step-end;
}

.fadeIn-enter .modal,
.fadeIn-leave-active.modal {
  transform: scale(1.1);
}
button {
  padding: 7px;
  margin-top: 10px;
  background-color: gray;
  color: white;
  font-size: 1.1rem;
}

.overlay {
  position: fixed;
  top: 0;
  left: 0;
  display: flex;
  justify-content: center;
  align-items: center;
  width: 100%;
  height: 100%;
  background: #00000094;
  z-index: 999;
  transition: opacity 0.2s ease;
}
</style>