<template>
  <div class="main">
    <div class="container">
      <div class="row">
        <div class="col-25">
          <label for="fname">First Name</label>
        </div>
        <div class="col-75">
          <input type="text" name="firstname" placeholder="Your name.." />
        </div>
      </div>
      <div class="row">
        <div class="col-25">
          <label for="lname">Last Name</label>
        </div>
        <div class="col-75">
          <input type="text" name="lastname" placeholder="Your last name.." />
        </div>
      </div>
      <div class="row">
        <div class="col-25">
          <label for="country">Country</label>
        </div>
        <div class="col-75">
          <select id="country" name="country">
            <option value="australia">Australia</option>
            <option value="canada">Canada</option>
            <option value="usa">USA</option>
          </select>
        </div>
      </div>
      <div class="row">
        <div class="col-25">
          <label for="subject">Subject</label>
        </div>
        <div class="col-75">
          <textarea
            id="subject"
            name="subject"
            placeholder="Write something.."
            style="height: 200px"
          ></textarea>
        </div>
      </div>
      <div class="row">
        <input type="submit" value="Submit" />
      </div>
    </div>
    <div class="action">
      <button class="btn-record" @click="startRecord()">Start record</button>
      <button
        class="btn-replay"
        :disabled="events.length < 2"
        @click="playRecord()"
      >
        Replay Record
      </button>
    </div>
    <div class="reset">
      <button @click="resetRecord()">Reset</button>
    </div>

    <div id="rrweb" class="replay"></div>
  </div>
</template>
<script>
import RrwebReplay from 'rrweb-player'
import { record } from 'rrweb'
export default {
  data() {
    return {
      events: [],
      recordFlag: false,
    }
  },
  methods: {
    startRecord() {
      this.recordFlag = true
      const self = this
      record({
        emit(event) {
          if (self.recordFlag) {
            self.events.push(event)
          }
        },
      })
    },
    playRecord() {
      const rrwebEl = document.getElementById('rrweb')
      // eslint-disable-next-line no-new
      new RrwebReplay({
        target: rrwebEl,
        data: {
          events: this.events,
          autoPlay: true,
        },
      })
    },
    resetRecord() {
      this.recordFlag = false
      this.events = []
      const replayEl = document.getElementsByClassName('rr-player')[0]
      if (replayEl) replayEl.remove()
    },
  },
}
</script>
<style>
.main {
  position: relative;
}
.replay {
  top: 0;
  left: 200px;
  position: absolute;
}
.action {
  padding-top: 20px;
  padding-bottom: 20px;
}

.container {
  max-width: 1000px;
}
* {
  box-sizing: border-box;
}

input[type='text'],
select,
textarea {
  width: 100%;
  padding: 12px;
  border: 1px solid #ccc;
  border-radius: 4px;
  resize: vertical;
}

label {
  padding: 12px 12px 12px 0;
  display: inline-block;
}

input[type='submit'] {
  background-color: #4caf50;
  color: white;
  padding: 12px 20px;
  border: none;
  border-radius: 4px;
  cursor: pointer;
  float: right;
}

input[type='submit']:hover {
  background-color: #45a049;
}

.container {
  border-radius: 5px;
  background-color: #f2f2f2;
  padding: 20px;
}

.col-25 {
  float: left;
  width: 25%;
  margin-top: 6px;
}

.col-75 {
  float: left;
  width: 75%;
  margin-top: 6px;
}

/* Clear floats after the columns */
.row:after {
  content: '';
  display: table;
  clear: both;
}

.rr-controller.svelte-dxnc1j.svelte-dxnc1j {
  width: 100%;
  height: 80px;
  background: #fff;
  display: flex;
  flex-direction: column;
  justify-content: space-around;
  align-items: center;
  border-radius: 0 0 5px 5px;
}
.rr-timeline.svelte-dxnc1j.svelte-dxnc1j {
  width: 80%;
  display: flex;
  align-items: center;
}
.rr-timeline__time.svelte-dxnc1j.svelte-dxnc1j {
  display: inline-block;
  width: 100px;
  text-align: center;
  color: #11103e;
}
.rr-progress.svelte-dxnc1j.svelte-dxnc1j {
  flex: 1;
  height: 12px;
  background: #eee;
  position: relative;
  border-radius: 3px;
  cursor: pointer;
  box-sizing: border-box;
  border-top: solid 4px #fff;
  border-bottom: solid 4px #fff;
}
.rr-progress.disabled.svelte-dxnc1j.svelte-dxnc1j {
  cursor: not-allowed;
}
.rr-progress__step.svelte-dxnc1j.svelte-dxnc1j {
  height: 100%;
  position: absolute;
  left: 0;
  top: 0;
  background: #e0e1fe;
}
.rr-progress__handler.svelte-dxnc1j.svelte-dxnc1j {
  width: 20px;
  height: 20px;
  border-radius: 10px;
  position: absolute;
  top: 2px;
  transform: translate(-50%, -50%);
  background: rgb(73, 80, 246);
}
.rr-controller__btns.svelte-dxnc1j.svelte-dxnc1j {
  display: flex;
  align-items: center;
  justify-content: center;
  font-size: 13px;
}
.rr-controller__btns.svelte-dxnc1j button.svelte-dxnc1j {
  width: 32px;
  height: 32px;
  display: flex;
  padding: 0;
  align-items: center;
  justify-content: center;
  background: none;
  border: none;
  border-radius: 50%;
  cursor: pointer;
}
.rr-controller__btns.svelte-dxnc1j button.svelte-dxnc1j:active {
  background: #e0e1fe;
}
.rr-controller__btns.svelte-dxnc1j button.active.svelte-dxnc1j {
  color: #fff;
  background: rgb(73, 80, 246);
}
.rr-controller__btns.svelte-dxnc1j button.svelte-dxnc1j:disabled {
  cursor: not-allowed;
}
.replayer-wrapper {
  position: relative;
}
.replayer-mouse {
  position: absolute;
  width: 20px;
  height: 20px;
  transition: 0.05s linear;
  background-size: contain;
  background-position: 50%;
  background-repeat: no-repeat;
  background-image: url('data:image/svg+xml;base64,PHN2ZyBoZWlnaHQ9IjMwMCIgd2lkdGg9IjMwMCIgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzIwMDAvc3ZnIiBkYXRhLW5hbWU9IkxheWVyIDEiIHZpZXdCb3g9IjAgMCA1MCA1MCI+PHBhdGggZD0iTTQ4LjcxIDQyLjkxTDM0LjA4IDI4LjI5IDQ0LjMzIDE4YTEgMSAwIDAwLS4zMy0xLjYxTDIuMzUgMS4wNmExIDEgMCAwMC0xLjI5IDEuMjlMMTYuMzkgNDRhMSAxIDAgMDAxLjY1LjM2bDEwLjI1LTEwLjI4IDE0LjYyIDE0LjYzYTEgMSAwIDAwMS40MSAwbDQuMzgtNC4zOGExIDEgMCAwMC4wMS0xLjQyem0tNS4wOSAzLjY3TDI5IDMyYTEgMSAwIDAwLTEuNDEgMGwtOS44NSA5Ljg1TDMuNjkgMy42OWwzOC4xMiAxNEwzMiAyNy41OEExIDEgMCAwMDMyIDI5bDE0LjU5IDE0LjYyeiIvPjwvc3ZnPg==');
}
.replayer-mouse:after {
  content: '';
  display: inline-block;
  width: 20px;
  height: 20px;
  border-radius: 10px;
  background: #4950f6;
  transform: translate(-10px, -10px);
  opacity: 0.3;
}
.replayer-mouse.active:after {
  animation: click 0.2s ease-in-out 1;
}
.replayer-mouse-tail {
  position: absolute;
  pointer-events: none;
}
@keyframes click {
  0% {
    opacity: 0.3;
    width: 20px;
    height: 20px;
    border-radius: 10px;
    transform: translate(-10px, -10px);
  }
  50% {
    opacity: 0.5;
    width: 10px;
    height: 10px;
    border-radius: 5px;
    transform: translate(-5px, -5px);
  }
}
.rr-player {
  position: relative;
  background: white;
  float: left;
  border-radius: 5px;
  box-shadow: 0 24px 48px rgba(17, 16, 62, 0.12);
}
.rr-player__frame {
  overflow: hidden;
}
.replayer-wrapper {
  float: left;
  clear: both;
  transform-origin: top left;
  left: 50%;
  top: 50%;
}
.replayer-wrapper > iframe {
  border: none;
}
.switch.svelte-1mmdovf.svelte-1mmdovf {
  height: 1em;
  display: flex;
  align-items: center;
}
.switch.disabled.svelte-1mmdovf.svelte-1mmdovf {
  opacity: 0.5;
}
.label.svelte-1mmdovf.svelte-1mmdovf {
  margin: 0 8px;
}
.switch.svelte-1mmdovf input[type='checkbox'].svelte-1mmdovf {
  position: absolute;
  opacity: 0;
}
.switch.svelte-1mmdovf label.svelte-1mmdovf {
  width: 2em;
  height: 1em;
  position: relative;
  cursor: pointer;
  display: block;
}
.switch.disabled.svelte-1mmdovf label.svelte-1mmdovf {
  cursor: not-allowed;
}
.switch.svelte-1mmdovf label.svelte-1mmdovf:before {
  content: '';
  position: absolute;
  width: 2em;
  height: 1em;
  left: 0.1em;
  transition: background 0.1s ease;
  background: rgba(73, 80, 246, 0.5);
  border-radius: 50px;
}
.switch.svelte-1mmdovf label.svelte-1mmdovf:after {
  content: '';
  position: absolute;
  width: 1em;
  height: 1em;
  border-radius: 50px;
  left: 0;
  transition: all 0.2s ease;
  box-shadow: 0px 2px 5px 0px rgba(0, 0, 0, 0.3);
  background: #fcfff4;
  animation: switch-off 0.2s ease-out;
  z-index: 2;
}
.switch
  input[type='checkbox']:checked
  + label.svelte-1mmdovf.svelte-1mmdovf:before {
  background: rgb(73, 80, 246);
}
.switch
  input[type='checkbox']:checked
  + label.svelte-1mmdovf.svelte-1mmdovf:after {
  animation: switch-on 0.2s ease-out;
  left: 1.1em;
}
</style>
