<script>
  import { onMount, afterUpdate } from 'svelte';
  import lottie from 'lottie-web';
  import animationData from './robot.json';

  // Lottie
  let animationContainer;
  let animationInstance;

  onMount(() => {
    animationInstance = lottie.loadAnimation({
      container: animationContainer,
      animationData,
    });
  });
</script>

<div
  bind:this={animationContainer}
  class="h-[224px] object-contain mx-auto"
/>
