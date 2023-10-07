<script>
	const url = new URL(location.href);
	const urlSearchParams = new URLSearchParams(url.search);

	const code = urlSearchParams.get('code');

	let copied = false;
	function copyCodeToClipboard() {
		if (!code?.length) return;

		navigator.clipboard.writeText(cmd).catch((e) => {
			console.error(e);
		});

		copied = true;
	}

	function onKeyPress(e) {
		if (e.code === 'Enter') {
			copyCodeToClipboard();
			e.preventDefault();
			e.stopPropagating();
		}
	}

	$: cmd = `/bl-set-clan-invitation-code auth_code:${code}`;
</script>

<svelte:head>
	<title>BeatLeader OAuth</title>
</svelte:head>

<section>
	{#if code?.length}
		<h1>Authorization code received</h1>
		<p>Now copy the following command for the bot and paste it in Discord</p>
		<pre>{cmd} <svg
				tabindex="0"
				on:click={copyCodeToClipboard}
				on:keypress={onKeyPress}
				role="button"
				aria-pressed="false"
				xmlns="http://www.w3.org/2000/svg"
				viewBox="0 0 24 24"
				><path
					d="M6.9998 6V3C6.9998 2.44772 7.44752 2 7.9998 2H19.9998C20.5521 2 20.9998 2.44772 20.9998 3V17C20.9998 17.5523 20.5521 18 19.9998 18H16.9998V20.9991C16.9998 21.5519 16.5499 22 15.993 22H4.00666C3.45059 22 3 21.5554 3 20.9991L3.0026 7.00087C3.0027 6.44811 3.45264 6 4.00942 6H6.9998ZM5.00242 8L5.00019 20H14.9998V8H5.00242ZM8.9998 6H16.9998V16H18.9998V4H8.9998V6Z"
				/></svg
			></pre>
		{#if copied}
			<div>Command copied to the clipboard!</div>
		{/if}
	{:else}
		<h1>Something went wrong</h1>
		<p>No authorization code found.</p>
	{/if}
</section>

<style>
	section {
		display: flex;
		flex-direction: column;
		align-items: center;
	}

	svg {
		width: 1em;
		height: 1em;
		cursor: pointer;
	}
</style>
