<template>
	<div>
		<h1>Question {{ active + 1 }}</h1>
		<p v-html="questions[active].question"></p>
		<ul class="quiz">
			<answer v-for="(answer, index) in questions[active].answer" :key="index" :answer="answer" :correct="correct" :answered="answered" v-model="tempAnswer" />
		</ul>
		<button @click="nextQuestion" v-if="answered">Next</button>
		<button :disabled="tempAnswer === ''" @click="submitAnswer" v-else>Answer</button>
	</div>
</template>

<script>
	import Answer from './Answer'

	export default {
		props: ['questions', 'submit', 'end'],
		components: {
			Answer,
		},
		data() {
			return {
				active: 0,
				answered: false,
				tempAnswer: ''
			}
		},
		computed: {
			correct() {
				return this.questions[this.active].correct_answer
			}
		},
		methods: {
			nextQuestion() {
				this.tempAnswer = ''
				this.answered = false

				if (this.active < this.questions.length - 1) {
					this.active++
				} else {
					this.active = 0
					this.end()
				}
			},
			submitAnswer() {
				if (this.correct !== this.tempAnswer) {
					window.navigator.vibrate(200)
				}

				this.answered = true
				this.submit(this.tempAnswer)
			}
		}
	}
</script>