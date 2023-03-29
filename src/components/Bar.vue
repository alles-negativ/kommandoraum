<script>

export default {
  props: ['bars'],
  data() {
    return {

    }
  },
}
</script>

<template>
  <div class="bars">
    <div 
        v-for="bar in bars" 
        :key="bar"
        >
          <div class="bar__wrapper">
              <p 
                class="bar" 
                :style="{maxHeight: bar.state.replace(/[^\d.-]/g, '') + '%'}"
              >
            </p>
        </div>
      </div>
    </div>      
</template>

<style scoped>

.bars {
  display: flex;
}

.bar__wrapper {
  display: flex;
  justify-content: center;
  align-items: flex-end;
  height: 500px;
  padding: 0px;
  width: 20px;
  border: 2px solid red;
  margin-right: -2px;
}
.bar {
  display: block;
  max-height: 0px;
  height: 100%;
  transition: max-height ease-in-out 0.5s;
  width: 20px;
  background-color: #8B0000;
  padding: 0px;
  margin: 0px;
}

</style>