<template>
	<div class="result">
		<h1>Result</h1>
		<div class="score">
			<div class="number">
				<span>Score</span>
				<span class="text">{{ score }}</span>
			</div>
			<div class="number">
				<span>Correct</span>
				<span class="text">{{ correct }}</span>
			</div>
		</div>
		<button @click="reset">New Game</button>
	</div>
</template>

<script>
	export default {
		props: ['score', 'correct', 'reset']
	}
</script>