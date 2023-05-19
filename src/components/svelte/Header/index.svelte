<script>
  import { slide } from 'svelte/transition';
  import { onMount, afterUpdate } from 'svelte';
  import lottie from 'lottie-web';
  import animationData from './menu.json';

  let key;
  let duration;

  let isOpen = false;

  // Lottie
  let animationContainer;
  let animationInstance;

  onMount(() => {
    animationInstance = lottie.loadAnimation({
      container: animationContainer,
      animationData,
      loop: false,
      autoplay: false,
    });
  });

  afterUpdate(() => {
    const startFrame = isOpen ? 0 : 26;
    const endFrame = isOpen ? 27 : 56;
    animationInstance.playSegments([startFrame, endFrame], true);
    animationInstance.setSpeed(1.5);
  });

  function toggleMenu() {
    isOpen = !isOpen;
  }
</script>

<header class="fixed bottom-0 py-8 grid place-items-center gap-8 w-full z-50">
  {#if isOpen}
    {#key key}
      <nav
        in:slide={{ duration, delay: duration }}
        out:slide={{ duration }}
        class="mx-auto backdrop-blur-lg bg-white/40 w-fit py-2 px-6 rounded-full font-semibold uppercase shadow"
      >
        <ul class="flex gap-6 group">
          <li>
            <a href="/articles" class="flex items-center gap-1 px-2 py-1 rounded-full hover:bg-black/10">
              <div class="border border-black rounded-full h-3 w-3" />
              <span>Articles</span>
            </a>
          </li>
          <li>
            <a href="/resources" class="flex items-center gap-1 px-2 py-1 rounded-full hover:bg-black/10">
              <div class="border border-black rounded-full h-3 w-3" />
              <span>Resources</span>
            </a>
          </li>
          <li>
            <a href="#" class="flex items-center gap-1 px-2 py-1 rounded-full hover:bg-black/10">
              <div class="border border-black rounded-full h-3 w-3" />
              <span>Contact</span>
            </a>
          </li>
        </ul>
      </nav>
    {/key}
  {/if}
  <div class="mx-auto flex items-center gap-8">
    <a href="/" class="bg-brand-green w-fit py-2 px-6 rounded-full font-semibold shadow hover:bg-brand-green/70 transition">hackitude.io</a>
    <button
      on:click={toggleMenu}
      class="flex items-center backdrop-blur-lg bg-white/40 w-fit py-2 px-6 rounded-full font-semibold uppercase shadow hover:bg-white/70 transition"
    >
      <div bind:this={animationContainer} class="h-8 w-8" />
      <span>Menu</span>
    </button>
  </div>
</header>
