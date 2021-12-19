<script>
	import Hoverable from './Hoverable.svelte';
	import Box from './Box.svelte';
	let qrCodeBicarb = '';
	let qrCodeAcid = '';
	$:acidMonth = qrCodeAcid.substring(20,22);
	$:acidDay = qrCodeAcid.substring(23,24);
	$:acidYear = 2000 + qrCodeAcid.substring(18,19);
	$:acidLotNumber = qrCodeAcid.substring(26);
	$:acidExpireDate = `${acidMonth}/${acidDay}/${acidYear}`;
</script>

<Hoverable let:hovering={activeAcid}>
	<input class:activeAcid id='acid' bind:value={qrCodeAcid} placeholder="Scan QR Code Here">
</Hoverable>

{#if qrCodeAcid.length > 0}
<pr>Lot Number:</pr>
<Box>
	<p>
		{acidLotNumber}
	</p>
</Box>
<pr>Expiration Date</pr>
<Box>
	<p>
		{acidExpireDate}
	</p>
</Box>
{/if}

<style>
	#acid {
		padding: 1em;
		margin: 0 0 1em 0;
		background-color: #EC7063;
		color: white;
	}
	
	::placeholder { /* Chrome, Firefox, Opera, Safari 10.1+ */
  color: white;
  opacity: 1; /* Firefox */
}
	
	:-ms-input-placeholder { /* Internet Explorer 10-11 */
  color: white;
}

::-ms-input-placeholder { /* Microsoft Edge */
  color: white;
}

	.activeAcid {
		background-color: #E74C3C;
		color: white;
	}
</style>