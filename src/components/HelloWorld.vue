<template>
  <div class="hello">
    <img v-if="currentImage" :src="currentImage.src"><br/>
    <input v-if="currentImage" v-model="answer" @change="onAnswer">
  </div>
</template>

<script>

import { vowImage } from './vowImage';

export default {
  name: 'HelloWorld',
  components: vowImage,
  data() {
    return {
      images: [
        { src: 'arrival.jpg', label: ['прибытие'] },
        { src: 'hive.jpg', label: ['рой','улей'] },
        { src: 'love.jpg', label: ['любовь','цветок'] },
        { src: 'black_garden.jpg', label: ['сад','черный сад','чёрный сад'] },
        { src: 'black_heart.jpg', label: ['чёрное сердце','черное сердце','клякса'] },
        { src: 'dread.jpg', label: ['дырка','скорбь'] },
        { src: 'darkness.jpg', label: ['тьма'] },
        { src: 'drink.jpg', label: ['чаша','напиток'] },
        { src: 'earth.jpg', label: ['земля'] },
        { src: 'fleet.jpg', label: ['пирамиды','флот'] },
        { src: 'forsaken.jpg', label: ['форсейкен','презренные'] },
        { src: 'gift.jpg', label: ['руки','передача'] },
        { src: 'guardian.jpg', label: ['гардиан','страж'] },
        { src: 'higher_dimension.jpg', label: ['','высшее измерение'] },
        { src: 'hive.jpg', label: ['глаза','улей'] },
        { src: 'light.jpg', label: ['свет'] },
        { src: 'love.jpg', label: ['цветок','любовь'] },
        { src: 'memory.jpg', label: ['мозг','память'] },
        { src: 'murder.jpg', label: ['япония','убийство'] },
        { src: 'pyramid.jpg', label: ['треугольник','пирамида'] },
        { src: 'savathun.jpg', label: ['вичквин','саватун'] },
        { src: 'stop.jpg', label: ['квадрат','стоп'] },
        { src: 'tower.jpg', label: ['баннер','башня'] },
        { src: 'traveler.jpg', label: ['странник'] },
        { src: 'witness.jpg', label: ['витнесс','свидетель'] },
        { src: 'worm.jpg', label: ['змея','червь'] },
        { src: 'worship.jpg', label: ['бог','поклонение'] },
      ],
      currentImage: { src: 'arrival.jpg', label: 'прибытие' },
      currentIndex: 0,
      answer: ''
    }
  },
  methods: {
    onAnswer() {
      if (this.answer === this.currentImage.label) {
        this.setNewQuestion();
      }
    },
    setNewQuestion() {
        this.answer = '';
        var newImageIndex = this.getRandomInt(this.images.length, this.currentIndex);
        this.currentImage = this.images[newImageIndex];
        this.currentIndex = newImageIndex;      
    },
    getRandomInt(max, exclude) {
      var res = Math.floor(Math.random() * max);
      while (res === exclude) {
        res = Math.floor(Math.random() * max);
      }
      return res;
    }
  },
  mounted() {
    this.setNewQuestion();
  },
  props: {
    msg: String
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>
