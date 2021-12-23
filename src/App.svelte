<script>
	import Hoverable from "./Hoverable.svelte";
	import BoxAcid from "./BoxAcid.svelte";
	import BoxBicarb from "./BoxBicarb.svelte";
	import { onMount } from "svelte";
	import CopyToClipboard from "svelte-copy-to-clipboard";
	let qrCodeBicarb = "";
	let qrCodeAcid = "";
	let focusInput;
	onMount(() => focusInput.focus());
	$: acidMonth = qrCodeAcid.substring(20, 22);
	$: acidDay = qrCodeAcid.substring(22, 24);
	$: acidYear = 20 + qrCodeAcid.substring(18, 20);
	$: acidLotNumber = qrCodeAcid.substring(26);
	$: acidExpireDate = `${acidMonth}/${acidDay}/${acidYear}`;
	$: bicarbMonth = qrCodeBicarb.substring(28, 30);
	$: bicarbDay = qrCodeBicarb.substring(30, 32);
	$: bicarbYear = 20 + qrCodeBicarb.substring(26, 28);
	$: bicarbLotNumber = qrCodeBicarb.substring(34);
	$: bicarbExpireDate = `${bicarbMonth}/${bicarbDay}/${bicarbYear}`;
</script>

<div class="width-restriction">
	<div>
		<Hoverable let:hovering={activeAcid}>
			<input class:activeAcid id='acid' bind:this={focusInput} bind:value={qrCodeAcid} placeholder="Scan Acid QR Code Here">
		</Hoverable>

		{#if qrCodeAcid.length > 0}
			<pr>
				Lot Number: 
				<CopyToClipboard text={acidLotNumber} let:copy>
      		<button on:click={copy}>
						Copy
					</button>
				</CopyToClipboard>
			</pr>
			<BoxAcid>
				<p>
					{acidLotNumber}
				</p>
			</BoxAcid>
			<pr>
				Expiration Date:
				<CopyToClipboard text={acidExpireDate} let:copy>
      		<button on:click={copy}>
						Copy
					</button>
				</CopyToClipboard>
			</pr>
			<BoxAcid>
				<p>
					{acidExpireDate}
				</p>
			</BoxAcid>
		{/if}
	</div>
	<div>
		<Hoverable let:hover={activeBicarb}>
			<input class:activeBicarb id='bicarb' bind:value={qrCodeBicarb} placeholder="Scan Bicarb QR Code Here">
		</Hoverable>

		{#if qrCodeBicarb.length > 0}
			<pr>
				Lot Number:
				<CopyToClipboard text={bicarbLotNumber} let:copy>
      		<button on:click={copy}>
						Copy
					</button>
				</CopyToClipboard>
			</pr>
			<BoxBicarb>
				<p>
					{bicarbLotNumber}
				</p>
			</BoxBicarb>
			<pr>
				Expiration Date:
				<CopyToClipboard text={bicarbExpireDate} let:copy>
      		<button on:click={copy}>
						Copy
					</button>
				</CopyToClipboard>
			</pr>
			<BoxBicarb>
				<p>
					{bicarbExpireDate}
				</p>
			</BoxBicarb>
		{/if}
	</div>
</div>

<style>
	#acid {
	  width: 300px;
	  padding: 1em;
	  margin: 0 0 1em 0;
	  background-color: #ec7063;
	  color: white;
	}

	#bicarb {
	  width: 300px;
	  padding: 1em;
	  margin: 0 0 1em 0;
	  background-color: #5dade2;
	  color: white;
	}

	::placeholder {
	  /* Chrome, Firefox, Opera, Safari 10.1+ */
	  color: white;
	  opacity: 1; /* Firefox */
	}

	:-ms-input-placeholder {
	  /* Internet Explorer 10-11 */
	  color: white;
	}

	::-ms-input-placeholder {
	  /* Microsoft Edge */
	  color: white;
	}

	.activeAcid {
	  background-color: #e74c3c;
	  color: white;
	}

	.activeBicarb {
	  background-color: #3498db;
	  color: white;
	}

	.width-restriction {
	  display: flex;
	  justify-content: center;
	  align-items: center;
	}
</style>