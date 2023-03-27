<template>
  <div class="timer" v-bind:class="{ active: isPlay }">
    <div class="timer__head">
      {{ this.time }}
    </div>
    <div class="timer__controls">
      <button class="btn btn__play" v-if="!isPlay" @click="play"></button>
      <button class="btn btn__paused" v-if="isPlay" @click="paused"></button>
      <button class="btn btn__stop" @click="stop"></button>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      time: '00:00:00',
      timeStart: null,
      timeStop: null,
      stoppedDuration: 0,
      timer: null,
      isPlay: false,
    }
  },

  methods: {
    play() {

      if (this.timeStart === null) {
        this.timeStart = new Date();
      }

      if (this.timeStop !== null) {
        this.stoppedDuration += (new Date() - this.timeStop);
      }

      this.isPlay = true;

      this.timer = setInterval(() => {
        let currentTime = new Date()
        let timeEnd = new Date(currentTime - this.timeStart - this.stoppedDuration)
        let hour = timeEnd.getUTCHours()
        let min = timeEnd.getUTCMinutes()
        let sec = timeEnd.getUTCSeconds()

        this.time =
          addPrefix(hour, 2) + ":" +
          addPrefix(min, 2) + ":" +
          addPrefix(sec, 2)
      }, 1000);

      function addPrefix(num, digit) {
        let zero = '';
        for (let i = 0; i < digit; i++) {
          zero += '0';
        }
        return (zero + num).slice(-digit);
      }

    },

    paused() {
      this.isPlay = false
      this.timeStop = new Date();
      clearInterval(this.timer);
    },

    stop() {
      this.isPlay = false;
      clearInterval(this.timer);
      this.stoppedDuration = 0;
      this.timeStart = null;
      this.timeStop = null;
      this.time = "00:00:00";
    },
  },
}
</script>

<style scoped>
.timer {
  background-color: #696969;
}

.active .timer__head {
  color: #fff;
}

.active .btn__play {
  border-left-color: #fff;
}

.active .btn__paused::before,
.active .btn__paused::after,
.active .btn__stop {
  background-color: #fff;
}

.paused .btn__paused::before,
.paused .btn__paused:after {
  background-color: #9e9e9e;
}

.paused .btn__paused:hover::before,
.paused .btn__paused:hover:after {
  background-color: #fff;
}

.timer__head {
  font-weight: 400;
  font-size: 22px;
  line-height: 21px;
  text-align: center;
  color: #9e9e9e;
  text-align: center;
  padding: 22px 5px;
  border-bottom: solid 1px #9e9e9e;

}

.timer__controls {
  display: flex;
  justify-content: space-between;
  padding: 20px 0;
  max-width: 75px;
  margin-left: auto;
  margin-right: auto;
}

.btn {
  cursor: pointer;
  width: 20px;
  height: 20px;
  border: 0;
  outline: none;
  transition: all .3s;
}

.btn:hover {
  color: #fff;
  border-left-color: #fff;
}

.btn__play {
  background-color: transparent;
  border-top: 10px solid transparent;
  border-bottom: 10px solid transparent;
  border-left: 17px solid #9e9e9e;
  border-right: 0px solid transparent;
}

.btn__paused {
  background-color: transparent;
  display: flex;
  justify-content: space-between;
  width: 10px;
}

.btn__paused::after {
  content: "";
  width: 3px;
  height: 100%;
  position: relative;
  background-color: #9e9e9e;
  transition: background-color .3s;

}

.btn__paused::before {
  content: "";
  width: 3px;
  height: 100%;
  position: relative;
  background-color: #9e9e9e;
  transition: background-color .3s;

}

.btn__stop {
  background-color: #9e9e9e;
}

.btn__stop:hover {
  background-color: #fff;
}
</style>