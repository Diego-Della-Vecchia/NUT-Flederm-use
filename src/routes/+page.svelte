<script lang="ts">
	let round = $state(0);

	let showing = $state(false);

	let rounds: { title: string; img: string; options: string[] }[] = [
		{
			title: 'Wie groß sind Fledermäuse?',
			img: 'https://www.fledermaus-bayern.de/files/upload/Biologie%20und%20Allgemeines/K%C3%B6perbau-Schema.jpg',
			options: ['1-5cm', '5-10cm', '10.23-15.67cm']
		},
		{
			title: 'Wie viel wiegen Fledermäuse?',
			img: 'https://www.fledermaus-bayern.de/files/upload/Biologie%20und%20Allgemeines/K%C3%B6perbau-Schema.jpg',
			options: ['200-400g', '500-800g', '2-200g']
		},
		{
			title: 'Wie alt werden Fledermäuse?',
			img: 'https://www.nistkasten-online.de/blog/wp-content/uploads/2024/06/Fledermaus-gefunden.jpeg',
			options: ['5-15 Jahre', '10-30 Jahre', '3-5 Jahre']
		},
		{
			title: 'Was essen Fledermäuse?',
			img: 'https://www.wwf-junior.de/fileadmin/user_upload/Tiere/1440_Fledermaeuse_Grosser_Abendsegler_Zaehne__c__imago_images.jpg',
			options: ['Insekten', 'Beeren', 'Tierblut']
		},
		{
			title: 'Wie gut können Fledermäuse sehen?',
			img: 'https://149363556.v2.pressablecdn.com/wp-content/uploads/2016/08/fledermaus-2.jpg',
			options: ['Sehr gut', 'Bischen', 'Gar nicht']
		},
		{
			title: 'Zu welcher Tierklasse gehören Fledermäuse?',
			img: 'https://d1g9li960vagp7.cloudfront.net/wp-content/uploads/2021/05/Wirbeltierklassen-Evolution-1024x576.jpg',
			options: ['Reptilien', 'Vögel', 'Säugetiere']
		}
	];

	let solutions: { text: string; index: number[] }[] = [
		{
			text: 'Ihr Körper ist selten länger als 5 Zentimeter.',
			index: [0] // Corresponds to "1-5"
		},
		{
			text: 'Eine Fledermaus wiegt etwa 2-200 Gramm.',
			index: [2] // Corresponds to "2-200G"
		},
		{
			text: 'Fledermäuse werden etwa 10-30 Jahre alt.',
			index: [1] // Corresponds to "10-30"
		},
		{
			text: 'Fledermäuse essen hauptsächlich Insekten oder sie ernähren sich Vegetarisch. Es gibt hingegen aber eine Art von Fledermäuse die Blut saugen daher stammt Dracula mytos von Dracula.',
			index: [0, 1, 2] // Corresponds to "Insekten, Beeren"
		},
		{
			text: 'Fledermäuse sind nicht blind, sondern können hell und dunkel unterscheiden.',
			index: [1] // Corresponds to "Bischen"
		},
		{
			text: 'Fledermäuse gehören tatsächlich zu der Tierklasse Säugetiere.',
			index: [2] // Corresponds to "Säugetiere"
		}
	];

	let score = $state(0);
</script>

<h1>Fledermaus Quiz</h1>
<h2>Score: {score}</h2>

{#if round < rounds.length}
	<h2>{rounds[round].title}</h2>
	<img src={rounds[round].img} alt="" />
	{#if !showing}
		<dv class="container">
			{#each rounds[round].options as option, i (option)}
				<button
					class="card"
					onclick={() => {
						if (solutions[round].index.includes(i)) {
							score += 100;
						} else {
							if (score != 0) {
								score -= 50;
							}
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
	<h2>Du hast gewonnen</h2>
{:else}
	<img src="https://i.ytimg.com/vi/WdFa450Kb1w/maxresdefault.jpg" alt="" />
	<h2>Du hast verloren</h2>
{/if}

<button
	class="reset"
	onclick={() => {
		round = 0;
		score = 0;
		showing = false;
	}}>Zurücksetzen</button
>

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

	.reset {
		display: block;
		border: #32a840 2px solid;
		background-color: white;
		margin: 20px auto;
		font-family: Arial, Helvetica, sans-serif;
		font-size: 20px;
		padding: 10px;
		border-radius: 10px;
	}
</style>
