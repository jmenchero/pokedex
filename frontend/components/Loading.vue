<template>
  <div class="centered">
    <div class="zoom">
      <img class="shake" src="@/assets/svg/tail.svg" />
    </div>
  </div>
</template>

<script>
export default {}
</script>

<style>
.centered {
  height: 100px;
  position: fixed;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
}

.zoom {
  height: 100%;
  animation: zoom 1s cubic-bezier(0.36, 0.07, 0.19, 0.97) 2.5s forwards;
  transform: scale(1);
  padding: 10px;
  overflow: hidden;
}

.shake {
  height: 100%;
  animation: shake 0.82s 3 cubic-bezier(0.36, 0.07, 0.19, 0.97) forwards;
  transform: translate3d(0, 0, 0);
}
</style>
