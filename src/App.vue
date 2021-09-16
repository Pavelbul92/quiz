<template>
  <div id="app">
    <section class="quiz">
    <div class="question" v-if="!quiz.finished">
      <p class="question__text">
        {{ question.text }}
      </p>
      <ul class="question__answers">
        <li v-for="(answer, index) in question.answers" :key="index">
          <label><input v-model="quiz.currentAnswer" name="question__option" type="radio" :value="index">{{ answer.text }}</label>
        </li>
      </ul>
      <div>
        <button class="question__button" @click="next()">{{ hasNextQuestion ? 'Next' : 'Finish'}}</button>
      </div>
    </div>

    <div class="results" v-if="quiz.finished">
      <p>Finished</p>
      <p>Correct answers <strong>{{ this.quiz.correctAnswers }}</strong>/{{ this.questions.length}}</p>
    </div>
    </section>
  </div>
</template>

<script>

export default {
  name: 'app',
  data() {
    return {
      questions: [
        {
          text: "What is the color of blood when it's inside your body?",
          answers: [
            { text: 'Blue', isCorrect: false},
            { text: 'White', isCorrect: false},
            { text: 'Red', isCorrect: true},
            { text: 'Green', isCorrect: false},
          ]
        },{
          text: "What is the fastest bird in the world?",
          answers: [
            { text: 'Bald Eagle', isCorrect: false},
            { text: 'Peregrine Falcon', isCorrect: true},
            { text: 'Hummingbird', isCorrect: false},
            { text: 'Raven', isCorrect: false},
          ]
        },{
          text: "What is the tallest waterfall in the world?",
          answers: [
            { text: 'Angel Falls, Venezuela', isCorrect: true},
            { text: 'Niagara Falls, New York', isCorrect: false},
            { text: 'Wailua Falls, Hawaii', isCorrect: false},
            { text: 'Sutherland Falls, New Zealand', isCorrect: false},
          ]
        }
      ],
      quiz: {
        currentQuestion: 0,
        currentAnswer: null,
        correctAnswers: 0,
        finished: false,
      }
    }
  },
  computed: {
    question(){
      return this.questions[this.quiz.currentQuestion]
    },
    hasNextQuestion(){
      return this.questions[this.quiz.currentQuestion + 1]
    }
  },
  methods: {
    next(){
      if (this.question.answers[this.quiz.currentAnswer].isCorrect){
        this.quiz.correctAnswers++;
      }
      this.quiz.currentAnswer = null;

      if (this.hasNextQuestion){
        this.quiz.currentQuestion++
      } else {
        this.quiz.finished = true;
      }
    },
  }
}
</script>

<style lang="scss">
  #app {
    width: 100%;
    height: 100vh;
    display: flex;
    justify-content: center;
    align-items: center;
  }

  .quiz {
    display: block;
    width: 40%;
    margin: 0 auto;
    background: #f7f7f7;
    border-radius: 10px;
    padding: 10px;
  }

  .question {
    &__text {
      font-weight: bold;
    }

    &__answers {
      list-style-type: none;
      padding: 0;

      li {
        margin-bottom: 5px;
      }
    }

    &__button {
      background: #009ac7;
      border: 1px solid #000;
      padding: 10px;
      color: #fff;
      text-transform: uppercase;
      border-radius: 10px;
      transition: all 0.1s ease-in-out;
      cursor: pointer;

      &:hover {
        background: #000;
        color: #fff;
      }
    }
  }
</style>
