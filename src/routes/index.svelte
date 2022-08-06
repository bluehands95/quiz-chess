<script>
	let endgame = false;
	let gameStarted;
	let questions = [
		{
			question: 'Who is the actual chess champion?',
			answers: ['Ian Nepmniatchi', 'Magnus Carlsen', 'Viswanathan Anand', 'Fabiano Caruana']
		},
		{
			question: 'How many squares are in a chess board?',
			answers: ['64', '84', '56', '120']
		},
		{
			question: 'We cant capture the king',
			answers: ['True', 'False']
		}
	];
	let answers = ['Magnus Carlsen', '64', 'True'];

	let currentQuestion = 0;
	let points = 0;

	function startGame() {
		points = 0;
		gameStarted = true;
		endgame = false;
	}
	function nextQuestion({ answer }) {
		if (answer == answers[currentQuestion]) {
			points++;
		}
		currentQuestion++;
		if (currentQuestion >= questions.length) {
			currentQuestion = 0;
			endgame = true;
			return;
		}
	}
</script>

<div class="bg-zinc-800 w-full justify-center flex p-4">
	<p class="text-xl text-white">Quizz Chess</p>
</div>

<div class="flex p-1 m-2">
	{#if !gameStarted}
		<button class="text-lg rounded-xl p-2 bg-zinc-800 text-white" on:click={startGame}
			>Start Game</button
		>
	{:else if endgame}
		<h1 class="p-2">Your result is {points}</h1>
		<button class="bg-zinc-800 rounded-xl p-2 text-white" on:click={startGame}>Play again</button>
	{:else}
		<div>
			<h1 class="py-2 bold text-2xl">{currentQuestion + 1} of {questions.length}</h1>
			<h1 class="text-2xl m-1">Question: {questions[currentQuestion].question}</h1>
			{#each questions[currentQuestion].answers as answer}
				<div class="flex">
					<button
						class="text-lg m-1 cursor-pointer border-2 rounded-lg p-1 border-zinc-800 text-gray-800 hover:bg-zinc-800 hover:text-white"
						on:click={nextQuestion({ answer })}>{answer}</button
					>
				</div>
			{/each}
		</div>
	{/if}
</div>
