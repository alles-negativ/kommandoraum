<script>

export default {
  props: ['lights'],
  data() {
    return {

    }
  }
}
</script>

<template>
    <div class="lights">
        <div 
            class="light__box"
            :class="light.state.replace('0', 'NULL')" 
            v-for="light in lights" 
            :key="light"
            >
        </div>
    </div>
</template>

<style scoped>

.lights {
  display: grid;
  grid-template-columns: 1fr 1fr 1fr 1fr 1fr 1fr;
  grid-template-rows: 1fr 1fr 1fr;
  gap: 3px;
}

.light__box {
    display: flex;
    border: 2px solid red;
    aspect-ratio: 1/1;
    width: 20px;
    background-color: #8B0000;
}

/* ON/OFF switches */
.OFF {
    background-color: black;
}

/* Meters that can go to 0 replaced with regex to make it NULL */
.NULL {
    background-color: black;
}

</style>