<template>
  <div class="popup" v-if="showPopUp">
    <div class="block">
      <div class="title">Warning</div>
      <div class="message">
        You are going to reset the counter press Ok to reset!
      </div>
      <div class="actions">
        <button class="green" @click="reset">Ok</button>
        <button class="red" @click="close">Cancel</button>
      </div>
    </div>
  </div>
  <div class="tasbeeh">
    <div class="press" @click="add">
      <div>
        <div class="total">
          {{ counted }}
        </div>
        <div class="rounds">
          <!-- 3 - Times -->
          {{ round > 1 ? round + " - Times" : round + " - Time" }}
        </div>
      </div>
    </div>
    <div class="actions">
      <div class="reset" @click="open">
        <span>Reset</span>
      </div>
      <div class="options" id="v-model-radiobutton">
        <input type="radio" id="one" value="99" v-model="option" />
        <label for="one">99</label>
        <br />
        <input type="radio" id="two" value="33" v-model="option" />
        <label for="two">33</label>
      </div>
    </div>
  </div>
</template>

<script>
import { ref } from "vue";

export default {
  name: "Home",
  setup() {
    const option = ref(99);
    const counted = ref(0);
    const round = ref(0);
    const showPopUp = ref(false);

    const close = () => {
      showPopUp.value = false;
    };

    const open = () => {
      showPopUp.value = true;
    };

    const reset = () => {
      counted.value = 0;
      round.value = 0;
      showPopUp.value = false;
    };

    const add = () => {
      counted.value++;
      if (counted.value > option.value) {
        round.value++;
        counted.value = 0;
      }
    };

    return {
      option,
      counted,
      round,
      showPopUp,
      close,
      open,
      reset,
      add,
    };
  },
};
</script>

<style lang="scss" scoped>
.tasbeeh {
  position: fixed;
  width: 100%;
  height: 100vh;
  background: radial-gradient(
      ellipse farthest-side at 76% 77%,
      rgba(245, 228, 212, 0.25) 4%,
      rgba(255, 255, 255, 0) calc(4% + 1px)
    ),
    radial-gradient(circle at 76% 40%, #fef6ec 4%, rgba(255, 255, 255, 0) 4.18%),
    linear-gradient(135deg, #ff0000 0%, #000036 100%),
    radial-gradient(ellipse at 28% 0%, #ffcfac 0%, rgba(98, 149, 144, 0.5) 100%),
    linear-gradient(180deg, #cd6e8a 0%, #f5eab0 69%, #d6c8a2 70%, #a2758d 100%);
  background-blend-mode: normal, normal, screen, overlay, normal;
  cursor: pointer;
  .press {
    position: relative;
    width: 100%;
    height: 100%;
    z-index: 2;
    display: grid;
    justify-content: center;
    align-items: center;
    user-select: none;
    .total {
      position: relative;
      width: 100px;
      height: 100px;
      border-radius: 50%;
      border: 2px solid lightgray;
      box-shadow: 0px 0px 10px 0px gray;
      font-size: 50px;
      display: flex;
      justify-content: center;
      align-items: center;
    }
    .rounds {
      position: absolute;
      top: 20px;
      left: 20px;
      width: fit-content;
      height: 50px;
      border-radius: 50%;
      // border: 2px solid lightgray;
      // box-shadow: 0px 0px 10px 0px gray;
      font-size: 20px;
      display: flex;
      justify-content: center;
      align-items: center;
    }
  }
  .actions {
    position: absolute;
    top: 20px;
    right: 20px;
    z-index: 3;
    .options {
      position: relative;
      padding: 10px;
      text-align: center;
    }
    .reset {
      position: relative;

      width: 100px;
      height: 50px;
      background: #00003620;
      border-radius: 10px;
      font-size: x-large;
      display: flex;
      justify-content: center;
      align-items: center;
      user-select: none;
      &:hover {
        background: #00003640;
      }
      &:active {
        background: #00003620;
      }
    }
  }
}

.popup {
  position: fixed;
  width: 100%;
  height: 100vh;
  background: #46464670;
  z-index: 5;
  display: flex;
  justify-content: center;
  align-items: center;
  .block {
    position: relative;
    width: 250px;
    background: #fff;
    border-radius: 10px;
    padding: 10px;
    .title {
      position: relative;
      font-weight: 700;
    }
    .message {
      position: relative;
      margin-top: 10px;
      margin-bottom: 10px;
    }
    .actions {
      position: relative;
      button {
        position: relative;
        border: 0;
        border-radius: 10px;
        padding: 10px 15px;
        margin: 5px;
      }
      .red {
        background: tomato;
        color: white;
      }
      .green {
        background: rgb(104, 230, 104);
        color: #464646;
      }
    }
  }
}

@media only screen and (max-width: 600px) {
  .tasbeeh {
    position: fixed;
  }
}
</style>
