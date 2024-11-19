<script lang="ts">
	let round = $state(0);

	let showing = $state(false);

	let rounds: { title: string; img: string; options: string[] }[] = [
		{
			title: 'Wie gross sind Fledermäuse',
			img: 'https://www.fledermaus-bayern.de/files/upload/Biologie%20und%20Allgemeines/K%C3%B6perbau-Schema.jpg',
			options: ['1-5cm', '5-10cm', '10-15cm']
		}
	];

	let solutions: { text: string; index: number }[] = [
		{
			text: 'Die in Deutschland lebenden Fledermäuse sind eher klein. Ihr Körper ist selten länger als 5 Zentimeter.',
			index: 0
		}
	];

	let score = $state(0);
</script>

<h1>Rette die Fledermäuse</h1>
<h2>Score: {score}</h2>

{#if round < rounds.length}
	<img src={rounds[round].img} alt="" />
	{#if !showing}
		<dv class="container">
			{#each rounds[round].options as option, i (option)}
				<button
					class="card"
					onclick={() => {
						if (i == solutions[i].index) {
							score += 100;
						} else {
							score -= 50;
						}
						showing = true;
						setTimeout(() => {
							showing = false;
							round++;
						}, 4000);
					}}
				>
					{option}
				</button>
			{/each}
		</dv>
	{:else}
		<div class="container">
			<div class="card">
				<h2>Lösung</h2>
				<p>{solutions[round].text}</p>
			</div>
		</div>
	{/if}
{:else if score > 300}
	<img src="https://i.ytimg.com/vi/WdFa450Kb1w/maxresdefault.jpg" alt="" />
	<h2>Du hast sie gerettet</h2>
{:else}
	<img src="https://i.ytimg.com/vi/WdFa450Kb1w/maxresdefault.jpg" alt="" />
	<h2>Du hast sie nicht gerettet</h2>
{/if}

<style>
	h1,
	h2 {
		text-align: center;
		font-family: Arial, Helvetica, sans-serif;
		color: #32a840;
	}

	h2 {
		color: black;
	}

	.container {
		display: flex;
		justify-content: space-around;
		flex-wrap: wrap;
		gap: 20px;
		padding-top: 50px;
	}

	.card {
		border: #32a840 2px solid;
		padding: 10px;
		border-radius: 10px;
		width: 80vw;
		max-width: 300px;
		animation: fly 0.2s ease-in forwards;
		background-color: white;
		transition: transform 0.2s ease-in-out;
		display: block;
		font-size: 30px;
	}

	.card:hover {
		transform: scale(1.1);
	}

	.card:active {
		transform: scale(1);
	}

	@keyframes fly {
		0% {
			transform: translateY(30%);
			opacity: 0;
		}
		100% {
			transform: translateY(0%);
			opacity: 1;
		}
	}

	img {
		width: 200px;
		margin: auto;
		border-radius: 10px;
		display: block;
	}

	p {
		font-family: Arial, Helvetica, sans-serif;
		text-align: center;
	}
</style>
