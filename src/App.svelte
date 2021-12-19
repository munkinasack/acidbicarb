<script>
	import Hoverable from './Hoverable.svelte';
	let qrCode = '';
</script>

<Hoverable let:hovering={active}>
	
	<input class:active bind:value={qrCode} placeholder="Scan QR Code Here">

</Hoverable>

<style>
	input {
		padding: 1em;
		margin: 0 0 1em 0;
		background-color: #eee;
	}

	.active {
		background-color: #ff3e00;
		color: white;
	}
</style>