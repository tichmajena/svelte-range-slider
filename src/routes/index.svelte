<script context="module">
  export const prerender = true;
</script>

<script>
  var exports = {};
  export let left = 0;
  export let top = 0;

  let moving = false;

  function onMouseDown() {
    moving = true;
  }

  function onMouseMove(e) {
    if (moving) {
      left += e.movementX;
      top += e.movementY;
    }
  }

  function onMouseUp() {
    moving = false;
  }

  function rect(e) {
    console.log(e.getBoundingClientRect());
  }
  // 	$: console.log(moving);
</script>

<svelte:window on:mouseup="{onMouseUp}" on:mousemove="{onMouseMove}" />

<div class="w-full h-screen p-10 flex items-center">
  <div use:rect class="h-8 w-full text-center pt-1 bg-slate-300 relative">
    Div A
    <div
      on:mousedown="{onMouseDown}"
      style="left: {left}px; top: {top}px;"
      class="absolute select-none cursor-move bg-green-700 text-white h-10 p-2"
    >
      Div B
    </div>
  </div>
</div>
