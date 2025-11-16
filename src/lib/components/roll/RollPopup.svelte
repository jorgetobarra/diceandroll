<script lang="ts">
  import { createEventDispatcher } from "svelte";
  import IntrigueString from "../utils/IntrigueString.svelte";
  export let names = [];
  let result = [];
  let index = 0;
  const dispatch = createEventDispatcher();

  $: {
    random(names);
  }

  const close = () => {
    dispatch("close");
  };

  const printNext = () => {
    index++;
  };

  const printAll = () => {
    index = result.length;
  };

  const random = (strings: string[]) => {
    for (let i = 0; i < strings.length * 10; i++) {
      const num1 = Math.floor(Math.random() * strings.length);
      const num2 = Math.floor(Math.random() * strings.length);
      const temp = strings[num1];
      strings[num1] = strings[num2];
      strings[num2] = temp;
    }
    result = strings[0] ? strings : [];
    index = 0;
    printNext();
  };
</script>

<div class="modal">
  <span class="close" on:click={close}>&times;</span>
  <div class="modal-content">
    <h1>Roll results</h1>
    <div class="button-container">
      <button on:click={printNext}> Next name </button>
      <button on:click={printAll}> Show all </button>
    </div>
    <p>Your result is</p>
    {#each result as name, i (name)}
      {#if i < index}
        <p style="font-size: 1.5rem;">
          <strong style="font-size: 1.2rem;">{i + 1}.</strong>
          <IntrigueString inString={name} />
        </p>
      {/if}
    {/each}
    <button on:click={() => random(names)} style="margin-block: 1rem">
      Randomize again
    </button>
  </div>
</div>

<style>
  p {
    margin: 0.5rem;
  }

  .modal {
    background-color: var(--background-color);
    margin: 15% auto;
    padding: 20px;
    border: 1px solid #888;
    width: 80%;
  }
  .modal-content {
    display: flex;
    flex-direction: column;
    align-items: center;
  }
  .button-container {
    flex-direction: row;
  }

  .close {
    color: #aaa;
    float: right;
    font-size: 28px;
    font-weight: bold;
  }

  .close:hover,
  .close:focus {
    color: black;
    text-decoration: none;
    cursor: pointer;
  }
</style>
