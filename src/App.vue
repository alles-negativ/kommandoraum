<script>
// import Light from './components/Light.vue'
// import Bar from './components/Bar.vue'

export default {
  // components: {
  //   Light,
  //   Bar
  // },
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
    runState2() {
      console.log("state 2")
      console.log(null, this.item_list.measuring[0].name)
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
  },
  // computed: {
  //   getLights() {
  //     const regex = new RegExp(/lights/);
  //     const items = this.items;
  //     const result = items.filter(item => item.label.match(regex));
  //     console.log(result);
  //     return (result);
  //   },
  //   getBars() {
  //     const regex = new RegExp(/bar/);
  //     const items = this.items;
  //     const result = items.filter(item => item.label.match(regex));
  //     console.log(result);
  //     return (result);
  //   },
  // },
  mounted() {
    this.getItems();
  },
  // created(){
  //   this.interval = setInterval(() =>{
  //     this.getItems()}, 1000)
  // }
}
</script>

<template>
  <div class="itemlist" v-for="item in items" :key="item">
    <p>{{ item.name }}</p>
    <button @click='changeState($event,item.name,100)'>on</button>
    <button @click='changeState($event,item.name,0)'>off</button>
    <button @click='changeState($event,item.name,"ON")'>on plug</button>
    <button @click='changeState($event,item.name,"OFF")'>off plug</button>
  </div>
  <!-- <div class="wrapper">
    <Light :lights="getLights"/>
    <Bar :bars="getBars"/>
  </div> -->
  <div class="container__state">
    <div class="state" @click="runState1">1</div>
    <div class="state" @click="runState2">2</div>
    <div class="state" @click="runState3">3</div>
    <div class="state" @click="runState4">4</div>
    <div class="state" @click="runState5">5</div>
    <div class="state" @click="turnAll(0)">OFF</div>
    <div class="state" @click="turnAll(1)">ON</div>
  </div>
</template>

<style scoped>
div {
  display: flex;
}

p {
  margin-right: 10px;
}

.itemlist {
  margin: 0px;
  font-size: 10px;
}

.container__state {
  display: flex;
}

.state {
  height: 100px;
  width: 100px;
  margin: 10px;
  background: white;
  color: black;
}

</style>
