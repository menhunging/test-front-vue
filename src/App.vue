<template>
  <div class="timers">
    <div class="timers__list" v-if="countTimers > 0">
      <div class="timers__item" v-for="time in countTimers">
        <Timer />
      </div>
      <div class="timers__item">
        <button class="timer__add" @click="addTimer">+</button>
      </div>
    </div>
    <div v-else>
      <h2>Сорри колличество таймеров установленно: <strong style="color:red">{{ countTimers }}</strong></h2>
    </div>
  </div>
</template>

<script>
import Timer from '@/components/Timer.vue';

export default {
  data() {
    return {
      countTimers: 4,
    }
  },

  methods: {
    addTimer() {
      this.countTimers += 1;
    }
  },

  components: {
    Timer,
  },
}

</script>

<style>
@font-face {
  font-family: "GothamPro";
  src: url("~@/assets/fonts/GothamPro.woff2") format("woff2"),
    url("~@/assets/fonts/GothamPro.woff") format("woff");
  font-weight: normal;
  font-style: normal;
  font-display: swap;
}

* {
  padding: 0;
  margin: 0;
  box-sizing: border-box;
  font-family: "GothamPro";
}

button {
  background: transparent;
  border: 0;
  transition: color .3s, background-color .3s;
}

body {
  background-color: #353638;
  color: #fff;
  font-family: "GothamPro";
}

.timers {
  max-width: 775px;
  margin-left: auto;
  margin-right: auto;
  padding: 75px 0;
}

.timers__list {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  margin: -22.5px -25px;
}

.timers__list .timers__item {
  margin: 22.5px 25px;
}

.timer__add:hover {
  background-color: #fff;
}

.timer__add {
  cursor: pointer;
  width: 100%;
  height: 100%;
  background-color: #696969;
  display: flex;
  align-items: center;
  justify-content: center;
  font-size: 40px;
  color: #9e9e9e;
  min-height: 126px;
}

@media (max-width:1023px) {
  .timers {
    max-width: 500px;
  }

  .timers__list {
    grid-template-columns: repeat(2, 1fr);
  }
}

@media (max-width:639px) {
  .timers {
    max-width: 225px;
  }

  .timers__list {
    grid-template-columns: 1fr;
  }
}
</style>
