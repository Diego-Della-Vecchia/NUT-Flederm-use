<script lang="ts">
	let round = $state(0);

	let showing = $state(false);

	let rounds: { title: string; body: { img: string; text: string } }[][] = [
		[
			{
				title: 'Test',
				body: {
					img: 'https://www.wwf-junior.de/fileadmin/user_upload/Tiere/1440_Fledermaeuse_Grosser_Abendsegler_Zaehne__c__imago_images.jpg',
					text: 'das ist ein Test'
				}
			},
			{
				title: 'Test',
				body: {
					img: 'https://www.wwf-junior.de/fileadmin/user_upload/Tiere/1440_Fledermaeuse_Grosser_Abendsegler_Zaehne__c__imago_images.jpg',
					text: 'das ist ein Test'
				}
			},
			{
				title: 'Test',
				body: {
					img: 'https://www.wwf-junior.de/fileadmin/user_upload/Tiere/1440_Fledermaeuse_Grosser_Abendsegler_Zaehne__c__imago_images.jpg',
					text: 'das ist ein Test'
				}
			}
		],
		[
			{
				title: 'Test',
				body: {
					img: 'https://www.wwf-junior.de/fileadmin/user_upload/Tiere/1440_Fledermaeuse_Grosser_Abendsegler_Zaehne__c__imago_images.jpg',
					text: 'das ist ein Test'
				}
			},
			{
				title: 'Test',
				body: {
					img: 'https://www.wwf-junior.de/fileadmin/user_upload/Tiere/1440_Fledermaeuse_Grosser_Abendsegler_Zaehne__c__imago_images.jpg',
					text: 'das ist ein Test'
				}
			},
			{
				title: 'Test',
				body: {
					img: 'https://www.wwf-junior.de/fileadmin/user_upload/Tiere/1440_Fledermaeuse_Grosser_Abendsegler_Zaehne__c__imago_images.jpg',
					text: 'das ist ein Test'
				}
			}
		]
	];

	let solutions: { text: string; index: number }[] = [
		{ text: 'String', index: 0 },
		{ text: 'String', index: 0 }
	];

	let score = $state(0);


</script>

<h1>Rette die Fledermäuse</h1>
<h2>Score: {score}</h2>

{#if round < rounds.length}
	<div class="container">
		{#if !showing}
			{#each rounds[round] as current, i (current)}
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
					<h2>{current.title}</h2>
					<img src={current.body.img} alt="" />
					<p>{current.body.text}</p>
				</button>
			{/each}
		{:else}
			<div class="card">
				<h2>Lösung</h2>
				<p>{solutions[round].text}</p>
			</div>
		{/if}
	</div>
{:else if score > 300}
	<h2>Du hast sie gerettet</h2>
{:else}
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
	}

	.card {
		border: #32a840 2px solid;
		padding: 10px;
		border-radius: 10px;
		width: 80vw;
		max-width: 300px;
		height: 150vw;
		max-height: 400px;
		animation: fly 0.2s ease-in forwards;
		background-color: white;
		transition: transform 0.2s ease-in-out;
		display: block;
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
		width: 80%;
		margin: auto;
		border-radius: 10px;
		display: block;
	}

	p {
		font-family: Arial, Helvetica, sans-serif;
		text-align: center;
	}
</style>
