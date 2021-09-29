<script>
  async function getRandomNumber() {
    await new Promise((resolve) => {
      setTimeout(() => resolve(), 1000);
    });
    const randomNumber = Math.random();

    if (randomNumber > 0.5) {
      return randomNumber;
    } else {
      throw new Error(randomNumber.toString());
    }
  }

  let promise = getRandomNumber();

  function handleClick() {
    promise = getRandomNumber();
  }
</script>

<button on:click={handleClick}> generate random number </button>

{#await promise}
  <p>...waiting</p>
{:then number}
  <p>The number is {number}</p>
{:catch error}
  <p style="color: red">{error.message}</p>
{/await}