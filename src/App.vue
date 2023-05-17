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
      items: {
        lamp: [
          { name: "lamp1", state: "OFF" },
          { name: "lamp2", state: "OFF" },
        ],
        measuring: [
          { name: "measuring1", state: 0 },
          { name: "measuring2", state: 0 },
        ],
      },
      sounds: new Audio(new URL('./assets/boom.mp3', import.meta.url).href)
    }
  },
  methods: {
    getItems() {
      const options = { method: 'GET'};
      

      fetch('http://10.0.1.4:8080/rest/items', options)
        .then(response => response.json())
        .then(response => this.items = response)
        .then(response => console.log(response))
        .catch(err => console.error(err));
    },
    changeState($event, itemName, state){
      const options = {method: 'POST', headers: {'Content-Type': 'text/plain'}, body: state};

      fetch('http://10.0.1.4:8080/rest/items/'+ itemName, options)
        // .then(response => response.json())
        .then(response => console.log(response))
        .catch(err => console.error(err));

    },
    runState1() {
      console.log("state 1")
      this.sounds.play()
    }
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
