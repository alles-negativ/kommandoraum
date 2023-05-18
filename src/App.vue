<script>

export default {
  data() {
    return {
      items: 0,
      interval: null,
      item_list: {
        lamp: [
          { name: "lights_1_Power_1", state: "OFF" },
          { name: "lights_1_Power_2", state: "OFF" },
          { name: "lights_2_Power_1", state: "OFF" },
          { name: "lights_2_Power_2", state: "OFF" },
          { name: "lights_3_Power_1", state: "OFF" },
          { name: "lights_3_Power_2", state: "OFF" },
          { name: "lights_4_Power_1", state: "OFF" },
          { name: "lights_4_Power_2", state: "OFF" },
          { name: "lights_schrank_5_Power_1", state: "OFF" },
          { name: "lights_schrank_5_Power_2", state: "OFF" },
        ],
        singularity: [
          { name: "light_singularity_online_Power", state: "OFF" },
        ],
        measuring: [
          { name: "schrank1_Brightness_1", state: 0 },
          { name: "schrank1_Brightness_2", state: 0 },
          { name: "schrank1_Brightness_3", state: 0 },
          { name: "schrank1_Brightness_4", state: 0 },
          { name: "schrank_2_Brightness_1", state: 0 },
          { name: "schrank_2_Brightness_2", state: 0 },
          { name: "schrank_2_Brightness_3", state: 0 },
          { name: "schrank_2_Brightness_4", state: 0 },
          { name: "schrank_4_5_Brightness_1", state: 0 },
          { name: "schrank_4_5_Brightness_2", state: 0 },
          { name: "schrank_4_5_Brightness_3", state: 0 },
          { name: "schrank_4_5_Brightness_4", state: 0 },
          { name: "schrank_5_Brightness_1", state: 0 },
          { name: "schrank_5_Brightness_2", state: 0 },
          { name: "schrank_5_Brightness_3", state: 0 },
          { name: "schrank_5_Brightness_4", state: 0 },
          { name: "schrank_8_Brightness_1", state: 0 },
          { name: "schrank_8_Brightness_2", state: 0 },
          { name: "schrank_8_Brightness_3", state: 0 },
          { name: "schrank_8_Brightness_4", state: 0 },
          { name: "schrank_9_Brightness_1", state: 0 },
          { name: "schrank_9_Brightness_2", state: 0 },
          { name: "schrank_9_Brightness_3", state: 0 },
          { name: "schrank_9_Brightness_4", state: 0 },
        ],
        buttons: {
          init: false,
          start: false,
          voltage: 0,
        },
      },
      timer: {
        time: 60,
        interval: 0,
      },
      sounds: new Audio(new URL('./assets/boom.mp3', import.meta.url).href)
    }
  },
  methods: {
    getItems() {
      const options = { method: 'GET'};
      
      fetch('http://10.68.254.173:8080/rest/items', options)
        .then(response => response.json())
        .then(response => this.items = response)
        .then(response => console.log(response))
        .catch(err => console.error(err));
    },
    getButtons() {
      const options = { method: 'GET'};
      
      fetch('http://10.68.254.173:8080/rest/items/buttons_control', options)
        .then(response => response.json())
        .then(response => {
          let value = parseInt(response.state.slice(0, -2))
          if (value >= 14) {
            if (this.item_list.buttons.voltage >= 14) {
              this.item_list.buttons.init = this.item_list.buttons.init
              this.item_list.buttons.start = this.item_list.buttons.start
            }
            else if (this.item_list.buttons.voltage >= 13) {
              this.item_list.buttons.init = !this.item_list.buttons.init
              this.item_list.buttons.start = this.item_list.buttons.start
            }
            else if (this.item_list.buttons.voltage >= 8) {
              this.item_list.buttons.init = this.item_list.buttons.init
              this.item_list.buttons.start = !this.item_list.buttons.start
            }
            else if (this.item_list.buttons.voltage >= 6) {
              this.item_list.buttons.init = !this.item_list.buttons.init
              this.item_list.buttons.start = !this.item_list.buttons.start
            }
          }
          else if (value >= 13) {
            if (this.item_list.buttons.voltage >= 14) {
              this.item_list.buttons.init = !this.item_list.buttons.init
              this.item_list.buttons.start = this.item_list.buttons.start
            }
            else if (this.item_list.buttons.voltage >= 13) {
              this.item_list.buttons.init = this.item_list.buttons.init
              this.item_list.buttons.start = this.item_list.buttons.start
            }
            else if (this.item_list.buttons.voltage >= 8) {
              this.item_list.buttons.init = !this.item_list.buttons.init
              this.item_list.buttons.start = !this.item_list.buttons.start
            }
            else if (this.item_list.buttons.voltage >= 6) {
              this.item_list.buttons.init = this.item_list.buttons.init
              this.item_list.buttons.start = !this.item_list.buttons.start
            }
          }
          else if (value >= 8) {
            if (this.item_list.buttons.voltage >= 14) {
              this.item_list.buttons.init = this.item_list.buttons.init
              this.item_list.buttons.start = !this.item_list.buttons.start
            }
            else if (this.item_list.buttons.voltage >= 13) {
              this.item_list.buttons.init = !this.item_list.buttons.init
              this.item_list.buttons.start = !this.item_list.buttons.start
            }
            else if (this.item_list.buttons.voltage >= 8) {
              this.item_list.buttons.init = this.item_list.buttons.init
              this.item_list.buttons.start = this.item_list.buttons.start
            }
            else if (this.item_list.buttons.voltage >= 6) {
              this.item_list.buttons.init = !this.item_list.buttons.init
              this.item_list.buttons.start = this.item_list.buttons.start
            }
          }
          else {
            if (this.item_list.buttons.voltage >= 14) {
              this.item_list.buttons.init = !this.item_list.buttons.init
              this.item_list.buttons.start = !this.item_list.buttons.start
            }
            else if (this.item_list.buttons.voltage >= 13) {
              this.item_list.buttons.init = this.item_list.buttons.init
              this.item_list.buttons.start = !this.item_list.buttons.start
            }
            else if (this.item_list.buttons.voltage >= 8) {
              this.item_list.buttons.init = !this.item_list.buttons.init
              this.item_list.buttons.start = this.item_list.buttons.start
            }
            else if (this.item_list.buttons.voltage >= 6) {
              this.item_list.buttons.init = this.item_list.buttons.init
              this.item_list.buttons.start = this.item_list.buttons.start
            }
          }
          // overwrite old voltage with new value
          this.item_list.buttons.voltage = value
          console.log(this.item_list.buttons)
        })
        .catch(err => console.error(err));
    },
    changeState($event, itemName, state){
      const options = {method: 'POST', headers: {'Content-Type': 'text/plain'}, body: state};

      fetch('http://10.68.254.173:8080/rest/items/'+ itemName, options)
        // .then(response => response.json())
        .then(response => console.log(response))
        .catch(err => console.error(err));

    },
    delay(milliseconds){
      return new Promise(resolve => {
          setTimeout(resolve, milliseconds)
      })
    },
    async runState1() {
      console.log("state 1")
      this.changeState(null, "sounditem_1", Math.random(100))
      console.log(null, this.item_list.measuring[0])
      this.changeState(null, this.item_list.measuring[0].name, "50")
      await this.delay(3000);
      this.changeState(null, this.item_list.measuring[1].name, "50")
    },
    async runState2() {
      console.log("state 2")
    },
    turnAll(state) {
      if (state == 0) {
        this.item_list.measuring.forEach((element) => {
          this.changeState(null, element.name, "0")
        });
        this.item_list.lamp.forEach((element) => {
          this.changeState(null, element.name, "OFF")
        });
        this.changeState(null, this.item_list.singularity[0].name, "OFF")
      }
      else {
        this.item_list.measuring.forEach((element) => {
          this.changeState(null, element.name, "100")
        });
        this.item_list.lamp.forEach((element) => {
          this.changeState(null, element.name, "ON")
        });
        this.changeState(null, this.item_list.singularity[0].name, "ON")
      }
    },
    start() {
      this.item_list.buttons.init = false
      this.item_list.buttons.start = false

      this.time.interval = setInterval(() => {
        if (this.timer.time === 0) {
          this.timer.time = 60
          clearInterval(this.time.interval)
        } else {
          this.timer.time--
        }             
      }, 1000)
    }
  },
  mounted() {
    this.getItems();
  },
  created(){
    this.interval = setInterval(() =>{
      this.getButtons()}, 100)
  }
}
</script>

<template>
  <div class="wrapper">
    <div class="grid">
      <!-- <div class="itemlist" v-for="item in items" :key="item">
        <p>{{ item.name }}</p>
        <button @click='changeState($event,item.name,100)'>on</button>
        <button @click='changeState($event,item.name,0)'>off</button>
        <button @click='changeState($event,item.name,"ON")'>on plug</button>
        <button @click='changeState($event,item.name,"OFF")'>off plug</button>
      </div> -->
        <div class="button__state--switch">
          <p class="switch__text">Start</p>
          <div 
          class="switch__colouring"
          :class="{ active: item_list.buttons.start }"
          >
          </div>
        </div>
        <div class="button__state--switch">
          <p class="switch__text">Init</p>
          <div 
            class="switch__colouring" :class="{ active: item_list.buttons.init }"
          >
          </div>
        </div>
        <div class="button__state--switch"></div>
        <div class="button__state--switch"></div>
        <div class="container__onoff">
          <div class="button__small--off" @click="turnAll(0)">OFF</div>
          <div class="button__small--on" @click="turnAll(1)">ON</div>
        </div>

        <div class="button__state" @click="runState1">1</div>
        <div class="button__state" @click="runState2">2</div>
        <div class="button__state" @click="runState3">3</div>
        <div class="button__state" @click="runState4">4</div>
        <div class="button__state" @click="runState5">5</div>

        <div class="button__state--empty">empty</div>
        <div class="button__state--empty">empty</div>
        <div class="button__state--empty">empty</div>
        <div class="button__state--timer">
          <p class="timer__text">
            <!-- {{ timer.time }} -->
          </p>
        </div>
        <div class="button__state--start" @click="start">Start</div>
    </div>
  </div>
</template>