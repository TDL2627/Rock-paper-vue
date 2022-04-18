<template>
  <div class="container">
  <button v-on:click="randomChoice()"> START </button>
  </div>
</template>

<script>
const choices = ["grass", "fire", "water"];
export default {
  data() {
    return {
      choice: ""
    };
  },
  methods: {
    randomChoice() {
	const randomChoiceIndex = Math.floor(Math.random() * choices.length);
	this.choice = choices[randomChoiceIndex];
	this.$emit('getChoice', this.choice);
    },
  }
};
</script>

<style scoped>
button {
margin-left:40%;
  margin-bottom: 20px;
  padding: 15px 32px;
  background-color: #4CAF50;
  display: inline-block;
  font-size: 16px;
  color: #fff;
  border-radius: 5px;
  cursor: pointer;
}
button:hover {
  background-color: #54e459;
}
</style>