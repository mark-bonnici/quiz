<template>
  <div :class="$style.question" ref="question">
    <strong>Question {{ questionNumber }}:</strong>
    <br />
    <strong>{{ question.text }}</strong>

    <ul :class="$style.answers" v-if="question.type === 'mc'">
      <li v-for="(mcanswer, index) in question.answers" :key="index">
        <input type="radio" :id="'answer' + index" name="currentQuestion" v-model="answer" :value="mcanswer" />
        <label :for="'answer' + index">{{ mcanswer }}</label>
        <div :class="$style.check"></div>
      </li>
    </ul>

    <button @click="submitAnswer" :class="$style.button">Answer</button>
  </div>
</template>

<script lang="ts">
import VueGrid from '../../shared/components/VueGrid/VueGrid.vue';
import VueGridRow from '../../shared/components/VueGridRow/VueGridRow.vue';
import VueGridItem from '../../shared/components/VueGridItem/VueGridItem.vue';
import VueHeadline from '../../shared/components/VueHeadline/VueHeadline.vue';

export default {
  name: 'Question',
  data() {
    return {
      answer: '',
    };
  },
  props: ['question', 'question-number'],
  methods: {
    submitAnswer() {
      this.$emit('answer', { answer: this.answer });
      this.answer = null;
    },
  },
  computed: {},
};
</script>

<style lang="scss" module>
@import '../../design-system';

.question {
  position: relative;
}

.question {
  top: $space-unit * 14;
  font-size: 2rem;
  line-height: 1.2em;

  @include mediaMin(tabletPortrait) {
    top: $space-unit * 24;
  }

  @include mediaMin(tabletLandscape) {
    top: $space-unit * 26;
  }
}

.answers {
  margin-top: 20px;
}

ul {
  list-style: none;
  padding: 0;
  overflow: auto;
  max-width: 500px;
  margin: 0 auto;
}
ul li {
  color: #fff;
  display: block;
  position: relative;
  float: left;
  width: 100%;
  height: 100px;
}
ul li input[type='radio'] {
  position: absolute;
  visibility: hidden;
}

ul li label {
  display: block;
  position: relative;
  font-weight: 300;
  font-size: 1.35em;
  padding: 25px 25px 25px 80px;
  margin: 10px auto;
  height: 30px;
  z-index: 9;
  cursor: pointer;
  -webkit-transition: all 0.25s linear;
}

ul li:hover label {
  color: #ffffff;
}

ul li .check {
  display: block;
  position: absolute;
  border: 5px solid #fff;
  border-radius: 100%;
  height: 35px;
  width: 35px;
  top: 30px;
  left: 20px;
  z-index: 5;
  transition: border 0.25s linear;
  -webkit-transition: border 0.25s linear;
}

ul li:hover .check {
  border: 5px solid #ffffff;
}

ul li .check::before {
  display: block;
  position: absolute;
  content: '';
  border-radius: 100%;
  height: 15px;
  width: 15px;
  top: 5px;
  left: 5px;
  margin: auto;
  transition: background 0.25s linear;
  -webkit-transition: background 0.25s linear;
}

input[type='radio']:checked ~ .check {
  border: 5px solid #0dff92;
}

input[type='radio']:checked ~ .check::before {
  background: #0dff92;
}

input[type='radio']:checked ~ label {
  color: #0dff92;
}

.button {
  top: auto;
  margin-top: 30px;
}
</style>
