<script>
  export let title;
</script>

<style>
  .input {
    border: none;
    background: none;
    padding: 0;
    margin: 0;
    font-size: 50px;
    color: #000000;
    width: 100%;
  }
</style>

<input class="input" type="text" bind:value={title} />
