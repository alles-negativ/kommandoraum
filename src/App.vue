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
      interval: null
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

</style>
