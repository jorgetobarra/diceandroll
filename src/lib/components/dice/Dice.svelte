<script lang="ts">
  let num: number = 0;
  let max = 6;
  const random = () => {
    num = Math.floor(Math.random() * max) + 1;
  };
</script>

<!--  -->
<div class="container">
  <h1>Dice</h1>
  <label for="maxNum">Max. number to randomize to</label>
  <input
    id="maxNum"
    name="maxNum"
    type="number"
    bind:value={max}
    class="input"
  />
  <p>Your random number is</p>
  <p style="font-size: 3rem;"><strong>{num}</strong></p>
  <button on:click={random}> Roll dice </button>
</div>

<style>
  .container {
    display: flex;
    flex-direction: column;
    align-items: center;
  }
  .input {
    border-radius: 10px;
    padding: 0.8rem;
    font-size: 1rem;
    margin-block: 1rem;
    border: solid 2px black;
    box-shadow: 0.5rem 0.5rem var(--shadow-color);
  }
</style>
