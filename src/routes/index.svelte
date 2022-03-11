<script context="module">
  export const prerender = true;
</script>

<script>
  var exports = {};
  export let leftB = 0;
  export let leftC = 0;
  export let top = 0;
  let right;
  let startX;
  let endX;
  let startXC;
  let endXC;
  let greenBox;
  let rightgreenBox;
  let leftThumbPressed = false;
  let rightThumbPressed = false;

  let moving = false;
  let movingC = false;

  // green div must stop move at the end and first on the gray div
  // If e.clientX is greater than 56 moving = false
  // rightmust be less than or equal to 784
  // Left must be greater than 56

  let movedNumber;
  function onMouseDown(e) {
    if (((e.target.id = greenBox), leftThumbPressed)) {
      console.log(e.target.id);
      moving = true;
    } else {
      console.log(e.target.id);
      (e.target.id = rightgreenBox), rightThumbPressed;
      movingC = true;
    }
    console.log(e.target.id);
    console.log(e.clientX);
    console.log(startX, endX);
    movedNumber = e.clientX;
    moving = true;
    movingC = true;
  }

  function onMouseMove(e) {
    // console.log(e.clientX);
    let leftThumb = greenBox.getBoundingClientRect();
    let rightThumb = rightgreenBox.getBoundingClientRect();
    let rightthumbStart = rightThumb.x;
    let rightthumbEnd = rightThumb.x + rightThumb.width;
    console.log(rightthumbStart, rightthumbEnd);
    if (movingC) {
      // && rightthumbStart <= startXC && rightthumbEnd >= endXC
      console.log(startX, endX, e.clientX, moving);
      console.log(rightgreenBox.getBoundingClientRect());
      console.log("I am moving");
      leftC += e.movementX;
      console.log(leftC);
    }

    let thumbStart = leftThumb.x;
    let thumbEnd = leftThumb.x + leftThumb.width;
    console.log(thumbStart, thumbEnd);
    if (moving && thumbStart >= startX && thumbEnd <= endX) {
      console.log(startX, endX, e.clientX, moving);
      console.log(greenBox.getBoundingClientRect());
      // top += e.movementY;
      console.log("I am moving");
      leftB += e.movementX;
    }
  }

  function onMouseUp() {
    moving = false;
    movingC = false;
  }

  function rect(e) {
    console.log(e);
    console.log(e.getBoundingClientRect());
    let rangeRect = e.getBoundingClientRect();
    startX = rangeRect.x;
    endX = rangeRect.x + rangeRect.width;
    startXC = rangeRect.x;
    endXC = rangeRect.x + rangeRect.width;
  }
  // 	$: console.log(moving);
</script>

<svelte:window on:mouseup={onMouseUp} on:mousemove={onMouseMove} />

<div class="w-full h-screen p-10 flex items-center">
  <div
    use:rect
    class="h-8 w-full text-center pt-1 bg-slate-300 relative flex flex-row justify-between"
  >
    Div A
    <div
      bind:this={greenBox}
      on:mousedown={onMouseDown}
      style="left: {leftB}px;  top: {top}px;"
      id="left_thumb"
      class="absolute select-none cursor-move bg-green-700 text-white h-10 p-2"
    >
      Div B
    </div>

    <div
      bind:this={rightgreenBox}
      on:mousedown={onMouseDown}
      style="left: {leftC}px;  top: {top}px;"
      id="right_thumb"
      class=" select-none cursor-move bg-green-700 text-white h-10 p-2"
    >
      Div C
    </div>
  </div>
  <div>{movedNumber}</div>
</div>
