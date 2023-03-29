<script>

export default {

  data() {
    return {
      items: 0,
      interval: null
    }
  },
  methods: {
    getItems() {
      const options = { method: 'GET'};

      fetch('http://10.0.1.2:8080/rest/items', options)
        .then(response => response.json())
        .then(response => this.items = response)
        .then(response => console.log(response))
        .catch(err => console.error(err));
    },
  },
  computed: {
    getLights() {
      const regex = new RegExp(/lights/);
      const items = this.items;
      const result = items.filter(item => item.label.match(regex));
      console.log(result);
      return (result);
    }
  },
  mounted() {
    this.getItems()
  },
  created(){
    this.interval = setInterval(() =>{
      this.getItems()}, 5000)
  }
}
</script>

<template>
  <div v-for="item in items" :key="item">
    <p>{{ item.name }}</p>
    <p 
      class="bar" 
      :style="{width: item.state.replace(/[^\d.-]/g, '') * 50 + 'px', transition: 0.5 + 's'}"
    >
      {{ item.state }}
    </p> 
    <p 
      class="tags">
      {{ item.label }}
    </p>
  </div>
  <div>{{ getLights }}</div>
</template>

<style scoped>
div {
  display: flex;
}

p {
  margin-right: 10px;
}

.state {
  color: blue;
}

.tags {
  color: red;
}

.bar {
  display: block;
  height: 20px;
  background-color: blue;
}

</style>
