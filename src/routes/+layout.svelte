<script>
	import './styles.css';
</script>

<svelte:head>
	<title>bl-bot</title>
</svelte:head>

<div class="app">
	<main>
		<slot />
	</main>
</div>

<style>
	.app {
		display: grid;
		grid-template-columns: 1fr;
		align-items: center;
		justify-content: center;
		min-height: 100vh;
	}

	main {
		display: flex;
		flex-direction: column;
		align-items: center;
		box-sizing: border-box;
	}
</style>
