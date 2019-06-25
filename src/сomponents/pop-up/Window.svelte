<script>
  import { onMount } from "svelte";
  import { createEventDispatcher } from "svelte";
  import Input from "./Input.svelte";
  import InputTime from "./InputTime.svelte";
  import Lever from "./Lever.svelte";
  import Button from "./Button.svelte";

  export let timer;
  let rawTime;

  function dragElement(elmnt) {
    var pos1 = 0,
      pos2 = 0,
      pos3 = 0,
      pos4 = 0;
    elmnt.onmousedown = dragMouseDown;
    // center
    elmnt.style.top = window.innerHeight / 2 - 325 + "px";
    elmnt.style.left = window.innerWidth / 2 - 260 + "px";

    function dragMouseDown(e) {
      e = e || window.event;
      // e.preventDefault();
      // get the mouse cursor position at startup:
      pos3 = e.clientX;
      pos4 = e.clientY;
      document.onmouseup = closeDragElement;
      // call a function whenever the cursor moves:
      document.onmousemove = elementDrag;
    }

    function elementDrag(e) {
      e = e || window.event;
      // e.preventDefault();
      // calculate the new cursor position:
      pos1 = pos3 - e.clientX;
      pos2 = pos4 - e.clientY;
      pos3 = e.clientX;
      pos4 = e.clientY;
      // set the element's new position:
      elmnt.style.top = elmnt.offsetTop - pos2 + "px";
      elmnt.style.left = elmnt.offsetLeft - pos1 + "px";
    }

    function closeDragElement() {
      // stop moving when mouse button is released:
      document.onmouseup = null;
      document.onmousemove = null;
    }
  }

  function toSecond(hms) {
    var a = hms.split(":");
    if (a.length == 3) {
      a[0] = parseInt(a[0]);
      a[1] = parseInt(a[1]);
      a[2] = parseInt(a[2].slice(0, 2));
      return +a[0] * 60 * 60 + +a[1] * 60 + +a[2];
    }
    return 0;
  }

  const dispatch = createEventDispatcher();
  const click = () => {
    timer.time = timer.type == "timer" ? 0 : toSecond(rawTime);
    dispatch("start");
  };
  onMount(() => {
    dragElement(document.getElementById("window"));
  });
</script>

<style>
  .window {
    position: absolute;
    z-index: 9;

    padding: 60px 35px 40px;
    box-sizing: border-box;
    max-width: 650px;
    background: #fefefe;
    box-shadow: 0px 5px 20px rgba(0, 0, 0, 0.05);
    border-radius: 10px;
  }
  .text {
    font-size: 50px;

    color: #000000;
  }
  .center {
    display: flex;
    align-items: center;
    justify-content: center;
  }
</style>

<div class="window" id="window">
  <div style="margin-bottom:50px;" onclick="event.stopPropagation()">
    <Input bind:title={timer.name} />
  </div>
  <div class="text" style="margin-bottom:55px;">Тип таймера</div>

  <div style="margin-bottom:80px;">
    <Lever first="Timer" second="Countdown" bind:type={timer.type} />
  </div>

  {#if timer.type == 'countdown'}
    <div class="center" style="margin-bottom:80px;">
      <InputTime bind:rawTime />
    </div>
  {/if}

  <div class="center">
    <Button title="СТАРТ" on:click={click} />
  </div>
</div>
