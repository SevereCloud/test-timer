<script>
  export let first;
  export let second;
  export let type;

  function changeType() {
    type = type == "countdown" ? "timer" : "countdown";
  }
</script>

<style>
  .lever {
    display: flex;
  }
  .back {
    position: relative;
    width: 156px;
    height: 50px;
    background: #f7f7f7;
    border: 1px solid #f5f5f5;
    box-sizing: border-box;
    border-radius: 100px;
    margin: 0 20px;

    cursor: pointer;
  }
  .text {
    font-size: 50px;

    color: #000000;
  }
  .round {
    position: absolute;
    width: 50px;
    height: 50px;
    border-radius: 25px;
    background: #00ffa3;
    transition: all 0.2s linear;
    left: 0;
  }
  .round.right {
    left: 106px;
    background: #ff0000;
  }
</style>

<div class="lever">
  <div class="text">{first}</div>
  <div class="back" on:click={changeType}>
    <div class="round" class:right={type == 'countdown'} />
  </div>
  <div class="text">{second}</div>
</div>
