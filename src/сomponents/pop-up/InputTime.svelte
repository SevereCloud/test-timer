<script>
  import { onMount } from "svelte";
  import IMask from "imask";
  export let rawTime;

  onMount(() => {
    let mask = IMask(document.getElementById("time-mask"), {
      mask: "HH:MM:SS",
      blocks: {
        HH: {
          mask: IMask.MaskedRange,
          from: 0,
          to: 99
        },
        MM: {
          mask: IMask.MaskedRange,
          from: 0,
          to: 59
        },
        SS: {
          mask: IMask.MaskedRange,
          from: 0,
          to: 59
        }
      }
    });
    mask.on("accept", () => {
      rawTime = mask.value;
    });
  });
</script>

<style>
  #time-mask {
    border: none;
    background: none;
    padding: 0;
    margin: 0;
    font-size: 50px;
    width: 200px;
  }
</style>

<div class="input">
  <input id="time-mask" type="text" value="00:00:00" />
</div>
