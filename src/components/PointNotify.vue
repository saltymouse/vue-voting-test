<template>
  <div class="point-notify">
    <div
      class="point__icon"
      v-bind:class="{ cast : item.cast }"
      @click="buttonClicked(item)" :item="item"
    >

    <span v-if="item.emoji">{{ item.emoji }}</span>
    <img v-if="item.icon" :src="item.icon">

    </div>
    <div class="point__count">{{item.count}}</div>
  </div>
</template>


<script>
export default {
  name: 'VoteButton', // how we reference the import from other components
  props: ['item'],
  data() {
    return {}
  },
  methods: {
    buttonClicked(button) {
      this.$emit('button-clicked', button); // custom event-listener name, data it will provide
    }
  }
}
</script>


<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>


.voting-button {
  cursor: pointer;
  margin: 0.2rem;
  font-size: 2rem;
  flex: 0 0 auto;
  text-align: center;
}

.voting-button__icon {
  user-select: none; /* it's a button... no selecting! */
  border-color: #ccc;
  border-width: 1px;
  border-style: solid;
  border-radius: 10rem;
  padding: 0.5rem;
  margin: 0 0 0.5rem;
  height: 2rem;
  width: 2rem;
  transition: 200ms all;
}

.voting-button__icon img {
  width: 100%;
  height: auto;
}

.voting-button__count {
  color: #999;
  transition: 200ms all;
}

.voting-button:hover .voting-button__icon {
  border-color: deeppink;
  transition: 200ms all;
}

.voting-button:hover .voting-button__count {
  color: deeppink;
  transition: 200ms all;
}

.cast {
  background: pink;
}

.cast.voting-button__icon {
  border-color: deeppink;
  transition: 200ms all;
}
</style>
