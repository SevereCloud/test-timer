<script>
  export let timer;

  // При обновлении timer.time, автоматически обновить time
  $: time = timeToText(timer.time);

  function timeToText(t) {
    let s = t;

    let h = parseInt(s / 3600);
    s -= h * 3600;
    let m = parseInt(s / 60);
    s -= m * 60;

    return (
      ("0" + h).slice(-2) +
      ":" +
      ("0" + m).slice(-2) +
      ":" +
      ("0" + s).slice(-2)
    );
  }
</script>

<style>
  .body {
    display: flex;
    align-items: baseline;
    cursor: pointer;
    width: 100%;
    max-width: 384px;
  }
  .time {
    font-size: 50px;
    color: #000000;
    margin-right: 26px;
  }
  .name {
    font-size: 18px;
    word-wrap: break-word;
  }
  .active .time {
    color: #00ffa3;
  }
  .stop .time {
    color: #ff0000;
  }
</style>

<div
  class="body"
  class:active={timer.active && timer.time > 0}
  class:stop={!timer.active && timer.time > 0}
  on:click={() => (timer.active = !timer.active)}>
  <div class="time">{time}</div>
  <div class="name">{timer.name}</div>
</div>
