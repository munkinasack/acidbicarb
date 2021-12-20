<script>
	import Hoverable from './Hoverable.svelte';
	import Box from './Box.svelte';
	let qrCodeBicarb = '';
	let qrCodeAcid = '';
	$:acidMonth = qrCodeAcid.substring(20,22);
	$:acidDay = qrCodeAcid.substring(22,24);
	$:acidYear = 20 + qrCodeAcid.substring(18,20);
	$:acidLotNumber = qrCodeAcid.substring(26);
	$:acidExpireDate = `${acidMonth}/${acidDay}/${acidYear}`;
	$:bicarbMonth = qrCodeBicarb.substring(28,30);
	$:bicarbDay = qrCodeBicarb.substring(30,32);
	$:bicarbYear = 20 + qrCodeBicarb.substring(26,28);
	$:bicarbLotNumber = qrCodeBicarb.substring(34);
	$:bicarbExpireDate = `${bicarbMonth}/${bicarbDay}/${bicarbYear}`
</script>

<Hoverable let:hovering={activeAcid}>
	<input class:activeAcid id='acid' bind:value={qrCodeAcid} placeholder="Scan Acid QR Code Here">
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

<Hoverable let:hover={activeBicarb}>
	<input class:activeBicarb id='bicarb' bind:value={qrCodeBicarb} placeholder="Scan Bicarb QR Code Here">
</Hoverable>

{#if qrCodeBicarb.length > 0}
<pr>Lot Number:</pr>
<Box>
	<p>
		{bicarbLotNumber}
	</p>
</Box>
<pr>Expiration Date</pr>
<Box>
	<p>
		{bicarbExpireDate}
	</p>
</Box>
{/if}

<style>
	#acid {
		width: 300px;
		padding: 1em;
		margin: 0 0 1em 0;
		background-color: #EC7063;
		color: white;
	}
	
	#bicarb {
		width: 300px;
		padding: 1em;
		margin: 0 0 1em 0;
		background-color: #5DADE2;
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
	
	.activeBicarb {
		background-color: #3498DB;
		color: white;
	}
</style>