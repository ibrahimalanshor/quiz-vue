<template>
	<div class="splash">
		<div class="image">
			<img src="../assets/student-colour-400px.png">
		</div>
		<h1>Quiz For You</h1>
		<p>
			Lorem ipsum, dolor, sit amet consectetur adipisicing elit. Nostrum, dignissimos veniam? Dolore
		</p>
		<button @click="start">Start</button>
	</div>
</template>

<script>
	export default {
		props: ['start']
	}
</script>