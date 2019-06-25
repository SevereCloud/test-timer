<script>
  import { onMount } from "svelte";
  import AddButton from "./сomponents/AddButton.svelte";
  import Timer from "./сomponents/Timer.svelte";
  import Window from "./сomponents/pop-up/Window.svelte";

  const rawTimers = localStorage.timers;
  let timers = rawTimers
    ? JSON.parse(rawTimers)
    : [
        {
          name: "Таймер",
          active: true,
          time: 15,
          type: "countdown"
        },
        {
          name: "Секундомер",
          active: true,
          time: 60,
          type: "timer"
        }
      ];

  let newTimer = {
    name: "Название",
    active: true,
    time: 0,
    type: "timer"
  }
  let openWindow = false;

  // Добавить таймер
  function addTimer() {
    openWindow = false;
    timers.push(clone(newTimer));
  }

  onMount(() => {
    const interval = setInterval(() => {
      // Обновление таймеров каждую секунду
      for (let i = 0; i < timers.length; i++) {
        if (timers[i].active) {
          if (timers[i].type == "countdown") {
            if (timers[i].time == 0) {
              timers[i].active = false;
              return;
            }
            timers[i].time--;
          } else {
            timers[i].time++;
          }
        }
      }
      localStorage.timers = JSON.stringify(timers);
    }, 1000);

    return () => {
      clearInterval(interval);
    };
  });

  function clone(src) {
    return Object.assign({}, src);
  }
</script>

<style>
  .timers {
    display: grid;
    grid-template-columns: 1fr 1fr;
    grid-gap: 24px;
    margin: 0 auto;
    max-width: 860px;
  }
  .background{
    position: absolute;
    top: 0;
    bottom: 0;
    left: 0;
    right: 0;
  }
  .clear{
    display: flex;
    text-align: center;
    margin: 100px auto;
  }
  .clear span{
    cursor: pointer;
    margin: auto;
  }
  .header{
    padding: 200px 32px 80px;
    font-family: Roboto;
    font-size: 50px;
    line-height: 59px;
    text-align: center;
  }
</style>


<div class="header">
  ПОСТАВЬ СВОЙ ТАЙМЕР
</div>

<div class="timers">
  {#each timers as timer}
    <Timer {timer}/>
  {/each}
</div>

{#if timers.length>0}
  <div class="clear">
    <span on:click={() => timers=[]}>Очистить все таймеры</span> 
  </div>
{/if}

{#if openWindow}
  <div class="background" on:click={() => (openWindow = false)}></div>
  <Window bind:timer={newTimer} on:start={addTimer} />
{/if}

<AddButton on:click={() => (openWindow = true)} />
