<script>

export default {
  data() {
    return {
      // OFF, PLAY, INIT, END, DOOM
      state: "OFF",
      items: 0,
      interval: null,
      stateStatus: [false, false, false, false, false],
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
            { name: "security_lights", state: "OFF" },
          ],
        },
      },
      timer: {
        time: 60,
        interval: 0,
        reset: 60,
      },
      doomsdayStatus: false,
      randomStatus: false,
      deskStatus: false,
      singularityStatus: false,
    }
  },
  methods: {
    getButtons() {
      const options = { method: 'GET'};
      
      fetch('http://10.68.254.173:8080/rest/items/sensor', options)
        .then(response => response.json())
        .then(response => {
          // let value = parseInt(response.state.slice(0, -2)
          let value = parseInt(response.state)
          // console.log(value)
          if (value >= 4000) {
            if (this.item_list.buttons.voltage >= 4000) {
              this.item_list.buttons.init = this.item_list.buttons.init
              if (this.item_list.buttons.init == true) {
                this.item_list.buttons.start = this.item_list.buttons.start
              }
            }
            else if (this.item_list.buttons.voltage >= 2500) {
              this.item_list.buttons.init = !this.item_list.buttons.init
              if (this.item_list.buttons.init == true) {
                this.item_list.buttons.start = this.item_list.buttons.start
              }
            }
            else if (this.item_list.buttons.voltage >= 1850) {
              this.item_list.buttons.init = this.item_list.buttons.init
              if (this.item_list.buttons.init == true) {
                this.item_list.buttons.start = !this.item_list.buttons.start
              }
            }
            else if (this.item_list.buttons.voltage >= 1400) {
              this.item_list.buttons.init = !this.item_list.buttons.init
              if (this.item_list.buttons.init == true) {
                this.item_list.buttons.start = !this.item_list.buttons.start
              }
            }
          }
          else if (value >= 2500) {
            if (this.item_list.buttons.voltage >= 4000) {
              this.item_list.buttons.init = !this.item_list.buttons.init
              if (this.item_list.buttons.init == true) {
                this.item_list.buttons.start = this.item_list.buttons.start
              }
            }
            else if (this.item_list.buttons.voltage >= 2500) {
              this.item_list.buttons.init = this.item_list.buttons.init
              if (this.item_list.buttons.init == true) {
                this.item_list.buttons.start = this.item_list.buttons.start
              }
            }
            else if (this.item_list.buttons.voltage >= 1850) {
              this.item_list.buttons.init = !this.item_list.buttons.init
              if (this.item_list.buttons.init == true) {
                this.item_list.buttons.start = !this.item_list.buttons.start
              }
            }
            else if (this.item_list.buttons.voltage >= 1400) {
              this.item_list.buttons.init = this.item_list.buttons.init
              if (this.item_list.buttons.init == true) {
                this.item_list.buttons.start = !this.item_list.buttons.start
              }
            }
          }
          else if (value >= 1850) {
            if (this.item_list.buttons.voltage >= 4000) {
              this.item_list.buttons.init = this.item_list.buttons.init
              if (this.item_list.buttons.init == true) {
                this.item_list.buttons.start = !this.item_list.buttons.start
              }
            }
            else if (this.item_list.buttons.voltage >= 2500) {
              this.item_list.buttons.init = !this.item_list.buttons.init
              if (this.item_list.buttons.init == true) {
                this.item_list.buttons.start = !this.item_list.buttons.start
              }
            }
            else if (this.item_list.buttons.voltage >= 1850) {
              this.item_list.buttons.init = this.item_list.buttons.init
              if (this.item_list.buttons.init == true) {
                this.item_list.buttons.start = this.item_list.buttons.start
              }
            }
            else if (this.item_list.buttons.voltage >= 1400) {
              this.item_list.buttons.init = !this.item_list.buttons.init
              if (this.item_list.buttons.init == true) {
                this.item_list.buttons.start = this.item_list.buttons.start
              }
            }
          }
          else {
            if (this.item_list.buttons.voltage >= 4000) {
              this.item_list.buttons.init = !this.item_list.buttons.init
              if (this.item_list.buttons.init == true) {
                this.item_list.buttons.start = !this.item_list.buttons.start
              }
            }
            else if (this.item_list.buttons.voltage >= 2500) {
              this.item_list.buttons.init = this.item_list.buttons.init
              if (this.item_list.buttons.init == true) {
                this.item_list.buttons.start = !this.item_list.buttons.start
              }
            }
            else if (this.item_list.buttons.voltage >= 1850) {
              this.item_list.buttons.init = !this.item_list.buttons.init
              if (this.item_list.buttons.init == true) {
                this.item_list.buttons.start = this.item_list.buttons.start
              }
            }
            else if (this.item_list.buttons.voltage >= 1400) {
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
      this.stateStatus[0] = true
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
      this.stateStatus[1] = true
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
      this.stateStatus[2] = true
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
      this.stateStatus[3] = true
      this.changeState(null, "sounditem_4", Math.random(100))
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
      this.stateStatus[4] = true
      this.changeState(null, "sounditem_5", Math.random(100))
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
    async randomMode() {
      console.log("random")
      var onOff = [
        "ON",
        "OFF"
      ];
      let randomItems = this.item_list.measuring.sort(() => .5 - Math.random()).slice(0, 24);
      let randomLights = this.item_list.lamp.sort(() => .5 - Math.random()).slice(0, 7);
      // console.log(this.item_list.lamp);
      randomItems.forEach((element) => {
        this.changeState(null, element.name, this.scale(Math.floor(Math.random() * 200 - 100)))
      });
      randomLights.forEach((element) => {
        var randomLight = Math.floor(Math.random()*onOff.length)
        this.changeState(null, element.name, onOff[randomLight])
        // console.log();
      });
    },
    scale (number) {
      if (number <= 0) {
        return 0
      }
      else if (number >= 80) {
        return 100
      }
      return number
    },
    async dramaticEnd() {
      //IN TO OUT
      //schrank 5 (links)
      this.changeState(null, "sounditem_7", Math.random(100))
      this.changeState(null, this.item_list.lamp[9].name, "ON")
      this.changeState(null, this.item_list.measuring[10].name, "100")
      this.changeState(null, this.item_list.measuring[11].name, "100")
      this.changeState(null, this.item_list.measuring[12].name, "100")
      
      //schrank 5 (rechts)
      this.changeState(null, "sounditem_7", Math.random(100))
      this.changeState(null, this.item_list.lamp[8].name, "ON")
      this.changeState(null, this.item_list.measuring[13].name, "100")
      this.changeState(null, this.item_list.measuring[14].name, "100")
      this.changeState(null, this.item_list.measuring[15].name, "100")
      
      await this.delay(1750);
      
      //schrank 4
      this.changeState(null, "sounditem_7", Math.random(100))
      this.changeState(null, this.item_list.measuring[8].name, "100")
      this.changeState(null, this.item_list.measuring[9].name, "100")
      
      await this.delay(1100);
      
      //schrank 2
      this.changeState(null, "sounditem_7", Math.random(100))
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
      this.changeState(null, "sounditem_7", Math.random(100))
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
      // this.randomMode()
      this.item_list.buttons.init = true
      this.randomStatus = true
    },
    async initSequence() {
      if (this.state == "INIT") {
        this.state = "PLAY"
        this.turnAll(0)
        await this.delay(500)
        this.changeState(null, this.item_list.singularity[0].name, "OFF")
      }
      else {
        this.state = "INIT"
        this.changeState(null, "sounditem_2", Math.random(100))
        this.turnAll(0)
        await this.delay(500)
        this.changeState(null, this.item_list.singularity[0].name, "ON")
      }
    },
    startSequence() {
      this.state = "END"
      clearInterval(this.timer.interval)
      this.timer.interval = 0
      this.timer.time = this.timer.reset
      this.item_list.buttons.init = false
      this.item_list.buttons.start = false
      this.stateStatus = [false, false, false, false, false]
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
        // this.changeState(null, this.item_list.singularity[0].name, "ON")
      }
    },
    start() {
      if (this.timer.interval == 0) {
        // reset switches
        this.state = "PLAY"
        this.item_list.buttons.init = false
        this.item_list.buttons.start = false
        this.stateStatus = [false, false, false, false, false]
        // start sound for sequence
        this.changeState(null, "sounditem_start_sound", Math.random(100))
        // start the timer
        this.timer.interval = setInterval(() => {
          if (this.timer.time === 0) {
            this.timer.time = this.timer.reset
            clearInterval(this.timer.interval)
            this.timer.interval = 0
            this.state = "OFF"
            this.item_list.buttons.init = false
            this.item_list.buttons.start = false
            this.stopSequence()
          } else {
            if (this.timer.time == 30) {
              this.changeState(null, "sounditem_30_seconds", Math.random(100))
            }
            if (this.timer.time == 10) {
              this.changeState(null, "sounditem_10_seconds", Math.random(100))
            }
            if (this.timer.time == 4) {
              this.changeState(null, "sounditem_3_seconds", Math.random(100))
            }
            if (this.timer.time == 3) {
              this.changeState(null, "sounditem_2_seconds", Math.random(100))
            }
            if (this.timer.time == 2) {
              this.changeState(null, "sounditem_1_second", Math.random(100))
            }
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
      if (this.state == "OFF") {
        this.turnAll(0)
        this.changeState(null, "desk_lamp_Power", "OFF")
        this.dramaticEnd()
      }
      else {
        this.doomsdayStatus = !this.doomsdayStatus
      }
    },
    deskSwitch() {
      if (this.deskStatus == false) {
        this.deskStatus = true
        this.changeState(null, "desk_lamp_Power", "ON")
      }
      else {
        this.deskStatus = false
        this.changeState(null, "desk_lamp_Power", "OFF")
      }
    },
    singularitySwitch() {
      if (this.deskStatus == false) {
        this.deskStatus = true
        this.changeState(null, "desk_lamp_Power", "ON")
      }
      else {
        this.deskStatus = false
        this.changeState(null, "desk_lamp_Power", "OFF")
      }
    },
    randomSwitch() {
      if (this.state == "OFF") {
        this.item_list.buttons.init = !this.item_list.buttons.init
      }
      this.randomStatus = !this.randomStatus
    },
    async stopSequence() {
      if (this.doomsdayStatus == true) {
        console.log("dramatic end")
        this.turnAll(0)
        this.changeState(null, "desk_lamp_Power", "OFF")
        await this.delay(7000);
        this.dramaticEnd()
      }
      else if (this.state == "END") {
        this.state = "OFF"
        this.turnAll(0)
        // this.changeState(null, "voice_" + (Math.floor(Math.random() * 5) + 2), Math.random(100))
        this.changeState(null, "voice_0", Math.random(100))
        console.log("yes end")
      }
      else {
        this.state = "OFF"
        this.turnAll(0)
        this.changeState(null, "voice_0", Math.random(100))
        console.log("no end")
      }
    }
  },
  mounted() {
  },
  created(){
    this.interval = setInterval(() =>{
      this.getButtons()
      console.log(this.state)
      if (this.state == "OFF") {
        if (this.item_list.buttons.init && !this.randomStatus) {
          this.randomStatus = true
        }
        else if (!this.item_list.buttons.init && this.randomStatus) {
          this.randomStatus = false
          this.turnAll(0)
        }
      }
      else if (this.state == "PLAY") {
        if (this.item_list.buttons.init == true) {
          this.initSequence()
        }
      }
      else if (this.state == "INIT") {
        if (this.item_list.buttons.init == false) {
          this.initSequence()
        }
        else if (this.item_list.buttons.start == true) {
          this.startSequence()
        }
      }
    }, 250)
    this.interval = setInterval(() =>{
      if (this.randomStatus) {
        this.randomMode()
      }
    }, 1000)
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
        <div class="button__state--security" @click="deskSwitch" 
          :class="{ active: this.deskStatus }">Desklamp</div>
        <div class="button__state--empty">empty</div>
        <div class="container__onoff">
          <div class="button__small--off" @click="turnAll(0)">OFF</div>
          <div class="button__small--on" @click="turnAll(1)">ON</div>
        </div>

        <div class="button__state" @click="runState1"
          :class="{ active: this.stateStatus[0] }">1</div>
        <div class="button__state" @click="runState2"
          :class="{ active: this.stateStatus[1] }">2</div>
        <div class="button__state" @click="runState3"
          :class="{ active: this.stateStatus[2] }">3</div>
        <div class="button__state" @click="runState4"
          :class="{ active: this.stateStatus[3] }">4</div>
        <div class="button__state" @click="runState5"
          :class="{ active: this.stateStatus[4] }">5</div>

        <div class="button__state--security" @click="securitySwitch" 
          :class="{ active: this.item_list.security.status }">Security</div>
        <div class="button__state--doomsday" @click="doomsdaySwitch"
          :class="{ active: this.doomsdayStatus }">Doomsday</div>
        <div class="button__state--random" @click="randomSwitch"
          :class="{ active: this.randomStatus }">Random</div>
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