<script>
  import { createEventDispatcher } from "svelte";
  const dispatch = createEventDispatcher();
  const click = () => dispatch("click");
  export let title;
</script>

<style>
  .button {
    background: #0075ff;
    border: 1px solid #f5f5f5;
    border-radius: 5px;
    padding: 11px 30px;

    font-family: Roboto;
    font-style: normal;
    font-weight: normal;
    font-size: 24px;
    color: #ffffff;

    user-select: none;
    cursor: pointer;
  }
  .button:active {
    background: rgb(0, 106, 226);
  }
</style>

<div class="button" on:click={click}>{title}</div>
