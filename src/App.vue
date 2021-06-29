<template>
  <div id="app">
    <scratch-card ref="scratchCard"
      v-slot="{ init }"
      :brushOptions="brush"
      :hideOptions="hide"
      getPercentageCleared
      @percentage-update="updatePoints"
    >
      <div class="wrapper">
        <img :src="require('./assets/picture.jpg')">
      </div>
    </scratch-card>
		<p align="center">You scratched {{ percentage }}% free.</p>
		<div @click="auto()" class="btn">Auto Scratch</div>
		<div @click="reload()" class="btn">ReLoad</div>
		<div @click="clear()" class="btn">Clear</div>
  </div>
</template>

<script>
import scratchCard from './components/scratch-card.vue';
import paperPattern from './assets/paint-coat.jpg';

export default {
  name: 'App',
  components: {
    scratchCard,
  },
  data() {
    return {
      percentage: 0,
      hide: {
        type: 'pattern',
        src: paperPattern,
        repeat: 'no-repeat',
      },
      brush: {
        size: 40,
        shape: 'round',
      },
    };
  },
  methods: {
		auto(){
			this.$refs['scratchCard'].autoScratch()
		},
		reload(){
			this.$refs['scratchCard'].init()
		},
		clear(){
			this.$refs['scratchCard'].clearArea()
		},
    updatePoints(percentage) {
      this.percentage = percentage;
    },
  },
};
</script>

<style>

.btn{
	margin: 20px auto;
	padding: 5px 0;
	background: #dedabf;
	border-radius: 3px;
	width: 120px;
	text-align: center;
}
img{
	width: 100%;
	height: 100%;
}
.wrapper{
	width: 100%;
}
.scratch-card-wrapper {
	margin: 80px auto;
	width: 70%;
	height:0; 
	padding-bottom:70%;
}
#app {
  width: 100%;
	height: 100vh;
  margin: 0 auto;
	padding: 0;
}
#app:before{
  content: '';
  display:table;
}
body {
	font-family: pingfang SC,helvetica neue,arial,hiragino sans gb,microsoft yahei ui,microsoft yahei,simsun,sans-serif;
  background: #FFFFFF;
	width: 100%;
	height: 100%;
  margin: 0;
	padding: 0;
	border: 0;
}
</style>
