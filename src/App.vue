<script>

export default {
  data() {
    return {
      items: 0,
      interval: null,
      initiated: false,
      started: false,
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
        security: {
          status: false,
          elements: [
            { name: "security_lights_Power", state: "OFF" },
          ],
        },
      },
      timer: {
        time: 20,
        interval: 0,
        reset: 20,
      },
      doomsdayStatus: false,
      sounds: new Audio(new URL('./assets/boom.mp3', import.meta.url).href)
    }
  },
  methods: {
    getButtons() {
      const options = { method: 'GET'};
      
      fetch('http://10.68.254.173:8080/rest/items/buttons_control', options)
        .then(response => response.json())
        .then(response => {
          let value = parseInt(response.state.slice(0, -2))
          if (value >= 14) {
            if (this.item_list.buttons.voltage >= 14) {
              this.item_list.buttons.init = this.item_list.buttons.init
              if (this.item_list.buttons.init == true) {
                this.item_list.buttons.start = this.item_list.buttons.start
              }
            }
            else if (this.item_list.buttons.voltage >= 13) {
              this.item_list.buttons.init = !this.item_list.buttons.init
              if (this.item_list.buttons.init == true) {
                this.item_list.buttons.start = this.item_list.buttons.start
              }
            }
            else if (this.item_list.buttons.voltage >= 8) {
              this.item_list.buttons.init = this.item_list.buttons.init
              if (this.item_list.buttons.init == true) {
                this.item_list.buttons.start = !this.item_list.buttons.start
              }
            }
            else if (this.item_list.buttons.voltage >= 6) {
              this.item_list.buttons.init = !this.item_list.buttons.init
              if (this.item_list.buttons.init == true) {
                this.item_list.buttons.start = !this.item_list.buttons.start
              }
            }
          }
          else if (value >= 13) {
            if (this.item_list.buttons.voltage >= 14) {
              this.item_list.buttons.init = !this.item_list.buttons.init
              if (this.item_list.buttons.init == true) {
                this.item_list.buttons.start = this.item_list.buttons.start
              }
            }
            else if (this.item_list.buttons.voltage >= 13) {
              this.item_list.buttons.init = this.item_list.buttons.init
              if (this.item_list.buttons.init == true) {
                this.item_list.buttons.start = this.item_list.buttons.start
              }
            }
            else if (this.item_list.buttons.voltage >= 8) {
              this.item_list.buttons.init = !this.item_list.buttons.init
              if (this.item_list.buttons.init == true) {
                this.item_list.buttons.start = !this.item_list.buttons.start
              }
            }
            else if (this.item_list.buttons.voltage >= 6) {
              this.item_list.buttons.init = this.item_list.buttons.init
              if (this.item_list.buttons.init == true) {
                this.item_list.buttons.start = !this.item_list.buttons.start
              }
            }
          }
          else if (value >= 8) {
            if (this.item_list.buttons.voltage >= 14) {
              this.item_list.buttons.init = this.item_list.buttons.init
              if (this.item_list.buttons.init == true) {
                this.item_list.buttons.start = !this.item_list.buttons.start
              }
            }
            else if (this.item_list.buttons.voltage >= 13) {
              this.item_list.buttons.init = !this.item_list.buttons.init
              if (this.item_list.buttons.init == true) {
                this.item_list.buttons.start = !this.item_list.buttons.start
              }
            }
            else if (this.item_list.buttons.voltage >= 8) {
              this.item_list.buttons.init = this.item_list.buttons.init
              if (this.item_list.buttons.init == true) {
                this.item_list.buttons.start = this.item_list.buttons.start
              }
            }
            else if (this.item_list.buttons.voltage >= 6) {
              this.item_list.buttons.init = !this.item_list.buttons.init
              if (this.item_list.buttons.init == true) {
                this.item_list.buttons.start = this.item_list.buttons.start
              }
            }
          }
          else {
            if (this.item_list.buttons.voltage >= 14) {
              this.item_list.buttons.init = !this.item_list.buttons.init
              if (this.item_list.buttons.init == true) {
                this.item_list.buttons.start = !this.item_list.buttons.start
              }
            }
            else if (this.item_list.buttons.voltage >= 13) {
              this.item_list.buttons.init = this.item_list.buttons.init
              if (this.item_list.buttons.init == true) {
                this.item_list.buttons.start = !this.item_list.buttons.start
              }
            }
            else if (this.item_list.buttons.voltage >= 8) {
              this.item_list.buttons.init = !this.item_list.buttons.init
              if (this.item_list.buttons.init == true) {
                this.item_list.buttons.start = this.item_list.buttons.start
              }
            }
            else if (this.item_list.buttons.voltage >= 6) {
              this.item_list.buttons.init = this.item_list.buttons.init
              if (this.item_list.buttons.init == true) {
                this.item_list.buttons.start = this.item_list.buttons.start
              }
            }
          }
          // overwrite old voltage with new value
          this.item_list.buttons.voltage = value
          // console.log(this.item_list.buttons)
        })
        .catch(err => console.error(err));
    },
    changeState($event, itemName, state){
      const options = {method: 'POST', headers: {'Content-Type': 'text/plain'}, body: state};

      fetch('http://10.68.254.173:8080/rest/items/'+ itemName, options)
        // .then(response => response.json())
        // .then(response => console.log(response))
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
      // console.log(null, this.item_list.measuring[0])
      this.changeState(null, this.item_list.measuring[0].name, Math.floor(Math.random() * 80)+20)
      this.changeState(null, this.item_list.lamp[8].name, "ON")
      await this.delay(Math.floor(Math.random() * 400)+200);
      this.changeState(null, this.item_list.measuring[1].name, Math.floor(Math.random() * 80)+20)
      await this.delay(Math.floor(Math.random() * 300)+100);
      this.changeState(null, this.item_list.measuring[22].name, Math.floor(Math.random() * 80)+20)
      await this.delay(Math.floor(Math.random() * 4000)+2000);
      this.changeState(null, this.item_list.measuring[15].name, Math.floor(Math.random() * 80)+20)
      this.changeState(null, this.item_list.measuring[6].name, Math.floor(Math.random() * 80)+20)
      await this.delay(Math.floor(Math.random() * 6000)+5000);
      this.changeState(null, this.item_list.lamp[4].name, "ON")
      
    },
    async runState2() {
      this.changeState(null, "sounditem_2", Math.random(100))
      this.changeState(null, this.item_list.lamp[0].name, "ON")
      await this.delay(Math.floor(Math.random() * 600)+500);
      this.changeState(null, this.item_list.measuring[2].name, Math.floor(Math.random() * 80)+20)
      this.changeState(null, this.item_list.measuring[20].name, Math.floor(Math.random() * 80)+20)
      await this.delay(Math.floor(Math.random() * 1000)+500);
      this.changeState(null, this.item_list.measuring[14].name, Math.floor(Math.random() * 80)+20)
      this.changeState(null, this.item_list.lamp[6].name, "ON")
      this.changeState(null, this.item_list.measuring[7].name, Math.floor(Math.random() * 80)+20)
      await this.delay(Math.floor(Math.random() * 3000)+500);
      this.changeState(null, this.item_list.measuring[21].name, Math.floor(Math.random() * 80)+20)
    },
    async runState3() {
      this.changeState(null, "sounditem_3", Math.random(100))
      this.changeState(null, this.item_list.lamp[7].name, "ON")
      await this.delay(Math.floor(Math.random() * 600)+100);
      this.changeState(null, this.item_list.measuring[18].name, Math.floor(Math.random() * 80)+20)
      this.changeState(null, this.item_list.measuring[8].name, Math.floor(Math.random() * 80)+20)
      await this.delay(Math.floor(Math.random() * 1300)+100);
      this.changeState(null, this.item_list.measuring[13].name, Math.floor(Math.random() * 80)+20)
      this.changeState(null, this.item_list.lamp[1].name, "ON")
      await this.delay(Math.floor(Math.random() * 3000)+100);
      this.changeState(null, this.item_list.measuring[3].name, Math.floor(Math.random() * 80)+20)
      this.changeState(null, this.item_list.measuring[23].name, Math.floor(Math.random() * 80)+20)
    },
    async runState4() {
      this.changeState(null, "sounditem_1", Math.random(100))
      this.changeState(null, this.item_list.lamp[3].name, "ON")
      this.changeState(null, this.item_list.measuring[19].name, Math.floor(Math.random() * 80)+20)
      await this.delay(Math.floor(Math.random() * 600)+100);
      this.changeState(null, this.item_list.measuring[9].name, Math.floor(Math.random() * 80)+20)
      this.changeState(null, this.item_list.measuring[12].name, Math.floor(Math.random() * 80)+20)
      this.changeState(null, this.item_list.lamp[9].name, "ON")
      await this.delay(Math.floor(Math.random() * 600)+100);
      this.changeState(null, this.item_list.measuring[16].name, Math.floor(Math.random() * 80)+20)
      await this.delay(Math.floor(Math.random() * 600)+100);
      this.changeState(null, this.item_list.measuring[4].name, Math.floor(Math.random() * 80)+20)
    },
    async runState5() {
      //actual state 5
      this.changeState(null, "sounditem_1", Math.random(100))
      this.changeState(null, this.item_list.lamp[5].name, "ON")
      await this.delay(Math.floor(Math.random() * 600)+100);
      this.changeState(null, this.item_list.measuring[11].name, Math.floor(Math.random() * 80)+20)
      this.changeState(null, this.item_list.lamp[2].name, "ON")
      await this.delay(Math.floor(Math.random() * 600)+100);
      this.changeState(null, this.item_list.measuring[17].name, Math.floor(Math.random() * 80)+20)
      this.changeState(null, this.item_list.measuring[5].name, Math.floor(Math.random() * 80)+20)
      await this.delay(Math.floor(Math.random() * 600)+100);
      this.changeState(null, this.item_list.measuring[10].name, Math.floor(Math.random() * 80)+20)
    },
    async dramaticEnd() {
      //IN TO OUT
      //schrank 5 (links)
      this.changeState(null, "sounditem_1", Math.random(100))
      this.changeState(null, this.item_list.lamp[9].name, "ON")
      this.changeState(null, this.item_list.measuring[10].name, "100")
      this.changeState(null, this.item_list.measuring[11].name, "100")
      this.changeState(null, this.item_list.measuring[12].name, "100")
      
      //schrank 5 (rechts)
      this.changeState(null, "sounditem_1", Math.random(100))
      this.changeState(null, this.item_list.lamp[8].name, "ON")
      this.changeState(null, this.item_list.measuring[13].name, "100")
      this.changeState(null, this.item_list.measuring[14].name, "100")
      this.changeState(null, this.item_list.measuring[15].name, "100")
      
      await this.delay(1750);
      
      //schrank 4
      this.changeState(null, "sounditem_1", Math.random(100))
      this.changeState(null, this.item_list.measuring[8].name, "100")
      this.changeState(null, this.item_list.measuring[9].name, "100")
      
      await this.delay(1100);
      
      //schrank 2
      this.changeState(null, "sounditem_1", Math.random(100))
      this.changeState(null, this.item_list.measuring[4].name, "100")
      this.changeState(null, this.item_list.measuring[5].name, "100")
      this.changeState(null, this.item_list.measuring[6].name, "100")
      this.changeState(null, this.item_list.measuring[7].name, "100")
      //schrank 8
      this.changeState(null, this.item_list.measuring[16].name, "100")
      this.changeState(null, this.item_list.measuring[17].name, "100")
      this.changeState(null, this.item_list.measuring[18].name, "100")
      this.changeState(null, this.item_list.measuring[19].name, "100")
      
      await this.delay(800);
      
      //schrank 1
      this.changeState(null, "sounditem_1", Math.random(100))
      this.changeState(null, this.item_list.measuring[0].name, "100")
      this.changeState(null, this.item_list.measuring[1].name, "100")
      this.changeState(null, this.item_list.measuring[2].name, "100")
      this.changeState(null, this.item_list.measuring[3].name, "100")
      //schrank 9
      this.changeState(null, this.item_list.measuring[20].name, "100")
      this.changeState(null, this.item_list.measuring[21].name, "100")
      this.changeState(null, this.item_list.measuring[22].name, "100")
      this.changeState(null, this.item_list.measuring[23].name, "100")
      //lamps
      this.changeState(null, this.item_list.lamp[0].name, "ON")
      this.changeState(null, this.item_list.lamp[1].name, "ON")
      this.changeState(null, this.item_list.lamp[2].name, "ON")
      this.changeState(null, this.item_list.lamp[3].name, "ON")
      this.changeState(null, this.item_list.lamp[4].name, "ON")
      this.changeState(null, this.item_list.lamp[5].name, "ON")
      this.changeState(null, this.item_list.lamp[6].name, "ON")
      this.changeState(null, this.item_list.lamp[7].name, "ON")
      //security
      this.changeState(null, this.item_list.security.elements[0].name, "ON")
      this.item_list.security.status = true
    },
    async initSequence() {
      this.initiated = true
      this.turnAll(0)
      await this.delay(1000)
      this.changeState(null, this.item_list.singularity[0].name, "ON")
    },
    startSequence() {
      this.started = true
      clearInterval(this.timer.interval)
      this.timer.interval = 0
      this.timer.time = this.timer.reset
      this.stopSequence()
      // do some magic
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
      if (this.timer.interval == 0) {
        // reset switches
        this.item_list.buttons.init = false
        this.item_list.buttons.start = false
        this.initiated = false
        this.started = false
        // start the timer
        this.timer.interval = setInterval(() => {
          if (this.timer.time === 0) {
            this.timer.time = this.timer.reset
            clearInterval(this.timer.interval)
            this.timer.interval = 0
            this.stopSequence()
          } else {
            this.timer.time--
        }             
      }, 1000)
      }
    },
    securitySwitch() {
      if (this.item_list.security.status == false) {
        this.item_list.security.status = true
        this.changeState(null, this.item_list.security.elements[0].name, "ON")
      }
      else {
        this.item_list.security.status = false
        this.changeState(null, this.item_list.security.elements[0].name, "OFF")
      }
    },
    doomsdaySwitch() {
      this.doomsdayStatus = !this.doomsdayStatus
    },
    async stopSequence() {
      if (this.doomsdayStatus == true) {
        console.log("dramatic end")
        this.turnAll(0)
        await this.delay(2000);
        this.dramaticEnd()
      }
      else if (this.item_list.buttons.start) {
        this.turnAll(0)
        console.log("yes end")
      }
      else {
        this.turnAll(0)
        console.log("no end")
      }
    }
  },
  mounted() {
  },
  created(){
    this.interval = setInterval(() =>{
      this.getButtons()
      if (this.item_list.buttons.init == true && !this.initiated) {
        this.initSequence()
      }
      if (this.item_list.buttons.start == true && !this.started) {
        this.startSequence()
      }
    }, 500)
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
        <div class="button__state--empty">empty</div>
        <div class="button__state--empty">empty</div>
        <div class="container__onoff">
          <div class="button__small--off" @click="turnAll(0)">OFF</div>
          <div class="button__small--on" @click="turnAll(1)">ON</div>
        </div>

        <div class="button__state" @click="runState1">1</div>
        <div class="button__state" @click="runState2">2</div>
        <div class="button__state" @click="runState3">3</div>
        <div class="button__state" @click="runState4">4</div>
        <div class="button__state" @click="dramaticEnd">5</div>

        <div class="button__state--security" @click="securitySwitch" 
          :class="{ active: this.item_list.security.status }">Security</div>
        <div class="button__state--doomsday" @click="doomsdaySwitch"
          :class="{ active: this.doomsdayStatus }">Doomsday</div>
        <div class="button__state--empty">empty</div>
        <div class="button__state--timer">
          <p class="timer__text">
            {{ timer.time }}
          </p>
        </div>
        <div 
          class="button__state--start"
          :class="{ active: timer.interval }"
          @click="start"
        >
          Start
        </div>
    </div>
  </div>
</template>