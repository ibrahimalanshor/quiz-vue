<template>
  <div id="app">
  
    <div v-if="loading" class="loading">Loading...</div>

    <div class="box" v-else>
      
      <splash :start="begin" v-if="!start" />


      <div v-else>
        <quiz :questions="questions" :submit="submit" :end="stop" v-if="!end" />

        <result :score="score" :correct="correct" :reset="reset" v-else />
      
      </div>


    </div>

  </div>
</template>

<script>
  import Splash from './components/Splash.vue'
  import Result from './components/Result.vue'
  import Quiz from './components/Quiz.vue'

  export default {
    components: {
      Splash,
      Result,
      Quiz
    },
    data() {
      return {
        start: false,
        end: false,
        loading: true,
        questions: [],
        answers: []
      }
    },
    computed: {
      correctAnswer() {
        const correct = this.questions.map(question => {
          return question.correct_answer
        })
        const answers = this.answers
        
        return correct.filter((answer, index) => answer === answers[index])
      },
      score() {
        const totalQuestion = this.questions.length

        let score = this.correctAnswer.length
        score = Math.round(score / totalQuestion * 100)

        return `${score}/100`
      },
      correct() {
        const totalQuestion = this.questions.length

        const totalCorrect = this.correctAnswer.length

        return `${totalCorrect}/${totalQuestion}`
      }
    },
    methods: {
      begin() {
        this.start = true
      },
      stop() {
        this.end = true
      },
      submit(answer) {
        this.answers.push(answer)
      },
      reset() {
        this.loading = true
        this.start = false
        this.end = false
        this.answers = []

        this.fetchApi()
      },
      async fetchApi() {
        try {
          const response = await fetch('https://opentdb.com/api.php?amount=10&category=18&difficulty=easy')
          const responseJson = await response.json()

          const data = responseJson.results.map(question => {
            question.answer = [question.correct_answer, ...question.incorrect_answers]

            return question
          })

          this.questions = data
          this.loading = false
        } catch (err) {
          console.log(err)
        }
      }
    },
    mounted() {
      this.fetchApi()
    }
  }
</script>

<style>
  #app {
    font-family: 'Lato', sans-serif;
  }
</style>