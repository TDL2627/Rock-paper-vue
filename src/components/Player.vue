<template>
  <div class="container">
    <div class="row">
      <div class="col-lg-4">
	<img type="button" class="img" src="../assets/grass.png" v-on:click="grassChosen()" />
      </div>
      <div class="col-lg-4">
  <img type="button" class="img" src="../assets/fire.png" v-on:click="fireChosen()" />
      </div>
      <div class="col-lg-4">
  <img type="button" class="img" src="../assets/water.png" v-on:click="waterChosen()" />
      </div>
    </div>
  </div>
</template>

<script>
export default {
  methods: {
    grassChosen() {
      this.$emit('getChoice', 'grass')
    },
    fireChosen() {
      this.$emit('getChoice', 'fire')
    },
    waterChosen() {
      this.$emit('getChoice', 'water')
    },
  }
};
</script>

<style scoped>
.img {
  margin: 20px;
  height:150px;
  width: 120px;
  border-radius: 10px
}
</style>