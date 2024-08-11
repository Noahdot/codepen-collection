<template>
  <div class="body">
    <div class="clock">
      <div class="hour">
        <div class="hr" id="hr" ref="hr"></div>
      </div>
      <div class="min">
        <div class="mn" id="mn" ref="mn"></div>
      </div>
      <div class="sec">
        <div class="sc" id="sc" ref="sc"></div>
      </div>
    </div>
  </div>
</template>

<script setup lang="ts">
import { ref, onMounted } from 'vue';

const deg = ref(6);
const hr = ref(null);
const mn = ref(null);
const sc = ref(null);

const startClock = () => {
  const updateClock = () => {
    let day = new Date();
    let hh = day.getHours() * 30;
    let mm = day.getMinutes() * deg.value;
    let ss = (day.getSeconds() + (Date.now() % 1000) / 1000) * deg.value;
    // let ss = day.getSeconds() * deg.value;

    hr.value.style.transform = `rotateZ(${hh + mm / 12}deg)`;
    mn.value.style.transform = `rotateZ(${mm}deg)`;
    sc.value.style.transform = `rotateZ(${ss}deg)`;

    requestAnimationFrame(updateClock);
  };

  // updateClock();
  // setInterval(() => updateClock(), 1000);
  updateClock();
  // requestAnimationFrame(updateClock);
}

onMounted(() => {
  startClock();
});
</script>

<style lang="scss" scoped>
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

.body {
  display: flex;
  justify-content: center;
  align-items: center;
  min-height: 100vh;
  background: #091921;

  .clock {
    width: 350px;
    height: 350px;
    display: flex;
    justify-content: center;
    align-items: center;
    background: url(./images/clock.png);
    background-size: cover;
    border: 4px solid #091921;
    border-radius: 50%;
    box-shadow: 0 -15px 15px rgba(255, 255, 255, 0.05),
                inset 0 -15px 15px rgba(255, 255, 255, 0.05),
                0 15px 15px rgba(0, 0, 0, 0.3),
                inset 0 -15px 15px rgba(0, 0, 0, 0.3);

    &:before {
      content: '';
      position: absolute;
      width: 15px;
      height: 15px;
      background: #fff;
      border-radius: 50%;
      z-index: 10000;
    }

    .hour, .min, .sec {
      position: absolute;
    }

    .hour, .hr {
      width: 160px;
      height: 160px;
    }

    .min, .mn {
      width: 190px;
      height: 190px;
    }

    .sec, .sc {
      width: 230px;
      height: 230px;
    }

    .hr, .mn, .sc {
      display: flex;
      justify-content: center;
      border-radius: 50%;
    }

    .hr:before {
      content: '';
      position: absolute;
      width: 8px;
      height: 80px;
      background: #ff105e;
      z-index: 10;
      border-radius: 6px 6px 0 0;
    }

    .mn:before {
      content: '';
      position: absolute;
      width: 4px;
      height: 90px;
      background: #fff;
      z-index: 11;
      border-radius: 6px 6px 0 0;
    }

    .sc:before {
      content: '';
      position: absolute;
      width: 2px;
      height: 150px;
      background: #fff;
      z-index: 12;
      border-radius: 6px 6px 0 0;
    }
  }
}
</style>