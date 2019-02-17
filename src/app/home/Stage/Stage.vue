<template>
  <div :class="$style.stage" ref="stage">
    <canvas :class="$style.canvas" ref="canvas"></canvas>

    <vue-grid>
      <vue-grid-row>
        <vue-grid-item class="vueGridItem">
          <div id="quiz">
            <div v-if="introStage">
              <vue-headline level="1" :class="$style.title">{{ title }}</vue-headline>
              <div :class="$style.subTitle">
                <p>Select the correct answer</p>
              </div>
              <button @click="startQuiz" :class="$style.button">Start Quiz</button>
            </div>

            <div v-if="questionStage">
              <question
                :question="questions[currentQuestion]"
                v-on:answer="handleAnswer"
                :question-number="currentQuestion + 1"
              ></question>
            </div>

            <div v-if="resultsStage">
              <vue-headline level="1" :class="$style.title">
                You got {{ correct }} right out of {{ questions.length }} questions.
              </vue-headline>
              <p :class="$style.title">Your percentage is {{ perc }}%.</p>
            </div>
          </div>
        </vue-grid-item>
      </vue-grid-row>
    </vue-grid>
  </div>
</template>

<script lang="ts">
import { CircleAnimation } from '../../shared/animations/CircleAnimation';
import VueGrid from '../../shared/components/VueGrid/VueGrid.vue';
import VueGridRow from '../../shared/components/VueGridRow/VueGridRow.vue';
import VueGridItem from '../../shared/components/VueGridItem/VueGridItem.vue';
import VueHeadline from '../../shared/components/VueHeadline/VueHeadline.vue';
import Question from '../../shared/components/Question/Question.vue';

const fetch = require('node-fetch');
const quizData = 'https://api.myjson.com/bins/btab6';

export default {
  components: { VueHeadline, VueGridItem, VueGridRow, VueGrid, Question },
  props: {
    disableParticles: {
      type: Boolean,
      required: true,
    },
  },
  data() {
    return {
      introStage: false,
      questionStage: false,
      resultsStage: false,
      title: '',
      questions: [],
      currentQuestion: 0,
      answers: [],
      correct: 0,
      perc: null,
    };
  },
  created() {
    fetch(quizData)
      .then((res: any) => res.json())
      .then((res: any) => {
        this.title = res.title;
        this.questions = res.questions;
        this.introStage = true;
      });
  },
  computed: {},
  methods: {
    startQuiz() {
      this.introStage = false;
      this.questionStage = true;
    },
    handleAnswer(e: any) {
      this.answers[this.currentQuestion] = e.answer;
      if (this.currentQuestion + 1 === this.questions.length) {
        this.handleResults();
        this.questionStage = false;
        this.resultsStage = true;
      } else {
        this.currentQuestion++;
      }
    },
    handleResults() {
      this.questions.forEach((a: any, index: any) => {
        if (this.answers[index] === a.answer) {
          this.correct++;
        }
      });
      this.perc = ((this.correct / this.questions.length) * 100).toFixed(2);
    },
    handleResize() {
      const canvas: HTMLCanvasElement = this.$refs.canvas;
      const stage: HTMLElement = this.$refs.stage;
      const stageRect: ClientRect =
        stage.getClientRects().length > 0
          ? stage.getClientRects().item(0)
          : ({
              width: 0,
              height: 0,
            } as ClientRect);

      canvas.width = stageRect.width;
      canvas.height = stageRect.height;
    },
  },
  beforeMount() {
    window.addEventListener('resize', this.handleResize);
  },
  mounted() {
    this.handleResize();

    if (!this.disableParticles) {
      CircleAnimation(this.$refs.canvas);
    }
  },
  beforeDestroy() {
    window.removeEventListener('resize', this.handleResize);
  },
};
</script>

<style lang="scss" module>
@import '../../shared/design-system';

.stage {
  min-height: 100vh;
  overflow: hidden;
  position: relative;
  text-align: center;
  color: $brand-text-color-inverse;
  background: #233f61;

  @include mediaMin(tabletPortrait) {
    min-height: 100vh;
  }
}

.canvas {
  min-height: 100vh;
  width: 100%;
  position: absolute;
  background-color: transparent;
  left: 0;
  top: 0;

  @include mediaMin(tabletPortrait) {
    min-height: 100vh;
  }
}

.title,
.subTitle,
button {
  text-shadow: 0 5px 10px rgba(0, 0, 0, 0.33);
  position: relative;
}

.title {
  top: $space-unit * 14;

  @include mediaMin(tabletPortrait) {
    top: $space-unit * 24;
  }

  @include mediaMin(tabletLandscape) {
    top: $space-unit * 26;
  }
}

.subTitle {
  top: $space-unit * 13;

  @include mediaMin(tabletPortrait) {
    top: $space-unit * 22;
  }

  @include mediaMin(tabletLandscape) {
    top: $space-unit * 24;
  }
}

button {
  top: $space-unit * 30;

  @include mediaMin(tabletPortrait) {
    top: $space-unit * 30;
  }

  @include mediaMin(tabletLandscape) {
    top: $space-unit * 30;
  }
  display: inline-block;
  border: none;
  padding: 2rem 4rem;
  margin: 0;
  text-decoration: none;
  background: #20d8c7;
  color: #ffffff;
  font-family: sans-serif;
  font-size: 3rem;
  cursor: pointer;
  text-align: center;
  transition: background 250ms ease-in-out, transform 150ms ease;
  -webkit-appearance: none;
  -moz-appearance: none;
}

button:hover,
button:focus {
  background: #0053ba;
}

button:focus {
  outline: 1px solid #fff;
  outline-offset: -4px;
}

button:active {
  transform: scale(0.99);
}
</style>
