<template>
  <div class="hello">
    <img v-if="currentImage" :src="currentImage.src" /><br />
    <input v-if="currentImage" v-model="answer" @input="onAnswer" />
    <div>
      <div class="margins">
        <span class="transparent-box">Hold shift to show hint</span>
      </div>
      <div v-if="showHint" class="margins">
        <span class="transparent-box">{{ hint }}</span>
      </div>
    </div>
  </div>
</template>

<script>
import vowImage from "./vowImage";

export default {
  name: "HelloWorld",
  components: vowImage,
  data() {
    return {
      locales: ["En", "Ru"],
      currentLocale: "En",
      images: [
        {
          src: "arrival.jpg",
          labels: {
            Ru: ["прибытие"],
            En: ["arrival"],
          },
        },
        {
          src: "black_garden.jpg",
          labels: {
            Ru: ["сад", "черный сад", "чёрный сад"],
            En: ["mountain", "black garden"],
          },
        },
        {
          src: "black_heart.jpg",
          labels: {
            Ru: ["чёрное сердце", "черное сердце", "клякса"],
            En: ["black heart"],
          },
        },
        {
          src: "dread.jpg",
          labels: {
            Ru: ["дырка", "скорбь"],
            En: ["dread"],
          },
        },
        {
          src: "darkness.jpg",
          labels: {
            Ru: ["тьма"],
            En: ["darkness"],
          },
        },
        {
          src: "drink.jpg",
          labels: {
            Ru: ["чаша", "напиток"],
            En: ["drink"],
          },
        },
        {
          src: "earth.jpg",
          labels: {
            Ru: ["земля"],
            En: ["earth"],
          },
        },
        {
          src: "entrance.jpg",
          labels: {
            Ru: ["капля", "вход"],
            En: ["enter", "entrance"],
          },
        },
        {
          src: "fleet.jpg",
          labels: {
            Ru: ["пирамиды", "флот"],
            En: ["fleet"],
          },
        },
        {
          src: "forsaken.jpg",
          labels: {
            Ru: ["форсейкен", "презренные"],
            En: ["scorn", "forsaken"],
          },
        },
        {
          src: "gift.jpg",
          labels: {
            Ru: ["руки", "передача"],
            En: ["hands", "gift"],
          },
        },
        {
          src: "guardian.jpg",
          labels: {
            Ru: ["гардиан", "страж"],
            En: ["guardian"],
          },
        },
        {
          src: "higher_dimension.jpg",
          labels: {
            Ru: ["казан", "высшее измерение"],
            En: ["ascendant plane"],
          },
        },
        {
          src: "hive.jpg",
          labels: {
            Ru: ["глаза", "улей"],
            En: ["hive"],
          },
        },
        {
          src: "light.jpg",
          labels: {
            Ru: ["свет"],
            En: ["light"],
          },
        },
        {
          src: "love.jpg",
          labels: {
            Ru: ["цветок", "любовь"],
            En: ["love", "flower"],
          },
        },
        {
          src: "memory.jpg",
          labels: {
            Ru: ["мозг", "память"],
            En: ["memory", "brain"],
          },
        },
        {
          src: "murder.jpg",
          labels: {
            Ru: ["япония", "убийство"],
            En: ["murder", "kill"],
          },
        },
        {
          src: "pyramid.jpg",
          labels: {
            Ru: ["треугольник", "пирамида"],
            En: ["pyramid"],
          },
        },
        {
          src: "savathun.jpg",
          labels: {
            Ru: ["вичквин", "саватун"],
            En: ["savathun"],
          },
        },
        {
          src: "stop.jpg",
          labels: {
            Ru: ["квадрат", "стоп"],
            En: ["stop"],
          },
        },
        {
          src: "tower.jpg",
          labels: {
            Ru: ["баннер", "башня"],
            En: ["tower"],
          },
        },
        {
          src: "traveler.jpg",
          labels: {
            Ru: ["странник"],
            En: ["traveler"],
          },
        },
        {
          src: "witness.jpg",
          labels: {
            Ru: ["витнесс", "свидетель"],
            En: ["witness"],
          },
        },
        {
          src: "worm.jpg",
          labels: {
            Ru: ["змея", "червь"],
            En: ["worm"],
          },
        },
        {
          src: "worship.jpg",
          labels: {
            Ru: ["бог", "поклонение"],
            En: ["worship"],
          },
        },
      ],
      currentImage: {},
      questionHistory: [],
      currentIndex: 0,
      answer: "",
      showHint: !1,
    };
  },
  computed: {
    hint: function () {
      return this.currentImage.labels[this.currentLocale].join(", ");
    },
  },
  methods: {
    onAnswer() {
      if (this.currentImage.labels[this.currentLocale].indexOf(this.answer) === -1) {
        return;
      }
      this.addCurrentQuestionToHistory();
      if (this.questionHistory.length === this.images.length) {
        this.clearHistory();
      }
      this.setNewQuestion();
    },
    currentQuestionIsInHistory() {
      return this.questionHistory.indexOf(this.currentIndex) > -1;
    },
    addCurrentQuestionToHistory() {
      this.questionHistory.push(this.currentIndex);
    },
    clearHistory() {
      this.questionHistory = [];
    },
    setNewQuestion() {
      this.answer = "";
      var e = this.getNewRandomQuestionIndex();
      this.currentImage = this.images[e];
      this.currentIndex = e;
    },
    getNewRandomQuestionIndex() {
      var e = Math.floor(Math.random() * this.images.length);
      while (e === this.currentIndex || this.questionHistory.indexOf(e) > -1)
        e = Math.floor(Math.random() * this.images.length);
      return e;
    },
    toggleHint(e) {
      this.showHint = null !== e ? e : !this.showHint;
    },
  },
  mounted() {
    this.setNewQuestion(),
      window.addEventListener("keydown", (e) => {
        "Shift" == e.key && this.toggleHint(!0);
      }),
      window.addEventListener("keyup", (e) => {
        "Shift" == e.key && this.toggleHint(!1);
      }),
      this.setNewQuestion();
  },
  props: {},
};
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
.transparent-box {
  background-color: rgba(200, 200, 200, 0.7);
  padding: 5px;
}
.margins {
  margin: 15px;
}
</style>
