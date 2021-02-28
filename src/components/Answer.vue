<template>
	<li>
		<label>
			<div class="question" :class="check(answer)">
				<input type="radio" name="answer" @change="$emit('change', answer)" :value="answer" v-model="tempAnswer" :disabled="answered">
				<span class="mark"></span>
				<span class="text" v-html="answer"></span>
			</div>
			<span class="label">{{ correct === answer ? 'Correct Answer' : 'Your Answer' }}</span>
		</label>
	</li>
</template>

<script>
	export default {
		props: ['answer', 'correct', 'answered', 'value'],
		model: {
			prop: 'value',
			event: 'change'
		},
		data() {
			return {
				tempAnswer: ''
			}
		},
		methods: {
			check(answer) {
				if (this.answered) {
					if (this.correct === answer) {
						return 'right'
					} else if (this.value === answer) {
						return 'wrong'
					}
				}
			}
		}
	}
</script>