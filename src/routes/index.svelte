<script lang="ts">
	async function getRandomNumber(throwError: boolean) {
		if (throwError) {
			throw new Error('error');
		} else {
			return 'ok';
		}
	}

	// with this line, everything works fine
	let promise = getRandomNumber(false);
	// with this line, dev server crashes on start
	// let promise = getRandomNumber(true);

	function getResponse() {
		promise = getRandomNumber(false);
	}
	function throwError() {
		promise = getRandomNumber(true);
	}
</script>

<button on:click={getResponse}> get response </button>
<button on:click={throwError}> throw error </button>

{#await promise}
	<p>...waiting</p>
{:then number}
	<p>The number is {number}</p>
{:catch error}
	<p style="color: red">{error.message}</p>
{/await}
