<template>
  <div class="background">
    <img class="pikachu-tail" src="@/assets/svg/tail.svg" />
  </div>
</template>

<script>
export default {}
</script>

<style>
.background {
  z-index: -1;
  height: 100px;
  position: fixed;
  top: 50%;
  left: 50%;
  animation: zoom 1s cubic-bezier(0.36, 0.07, 0.19, 0.97) forwards;
  animation-delay: 2.5s;
  transform: scale(1);
  overflow: hidden;
}

.pikachu-tail {
  height: 100%;
  animation: shake 0.82s 3 cubic-bezier(0.36, 0.07, 0.19, 0.97) both;
  transform: translate3d(0, 0, 0);
}

@keyframes shake {
  10%,
  90% {
    transform: translate3d(-1px, 2px, 0);
  }
  0%,
  20%,
  80% {
    transform: translate3d(2px, -1px, 0);
  }
  30%,
  50%,
  70% {
    transform: translate3d(-4px, 4px, 0);
  }
  100%,
  40%,
  60% {
    transform: translate3d(4px, -4px, 0);
  }
}

@keyframes zoom {
  0% {
    transform: scale(1);
  }
  100% {
    transform: scale(2000);
  }
}
</style>
