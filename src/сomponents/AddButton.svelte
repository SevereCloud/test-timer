<script>
  import { createEventDispatcher } from 'svelte';
  const dispatch = createEventDispatcher();
  const click = () => dispatch('click');
</script>

<style>
  .button{
    position: absolute;
    width: 130px;
    height: 130px;
    left: -20px;
    top: -30px;
    border-radius:50%;

    background: #00FFA3;

    cursor: pointer;
  }
  .button::before{
    content: '+';
    position: absolute;
    left: 55px;
    top: 45px;
    text-align:center;
    font-family: Roboto;
    font-style: normal;
    font-weight: normal;
    font-size: 50px;
    line-height: 50px;

    color: #000000;
  
  }
  .button:active{
    background: rgb(0, 221, 140);
  }
</style>

<div class="button" on:click={click}>
  +
</div>