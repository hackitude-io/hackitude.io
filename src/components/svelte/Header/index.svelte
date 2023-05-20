<script>
  import { slide } from 'svelte/transition';
  import { onMount, afterUpdate } from 'svelte';
  import lottie from 'lottie-web';
  import animationData from './menu.json';
  import Logo from '../SVG/Logo.svelte';

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

  let isFirstLoad = true;

  afterUpdate(() => {
    if (animationInstance && !isFirstLoad) {
      const startFrame = isOpen ? 0 : 26;
      const endFrame = isOpen ? 27 : 56;
      animationInstance.playSegments([startFrame, endFrame], true);
      animationInstance.setSpeed(1.5);
    }
  });

  function toggleMenu() {
    isFirstLoad = false;
    isOpen = !isOpen;
  }

  function closeMenu(event) {
    if (
      event.key === 'Escape' ||
      !event.target.closest('.backdrop-blur-lg')
    ) {
      isOpen = false;
    }
  }

  onMount(() => {
    document.addEventListener('keydown', closeMenu);
    document.addEventListener('click', closeMenu);
  });

  afterUpdate(() => {
    if (isOpen) {
      document.addEventListener('keydown', closeMenu);
      document.addEventListener('click', closeMenu);
    } else {
      document.removeEventListener('keydown', closeMenu);
      document.removeEventListener('click', closeMenu);
    }
  });
</script>

<header
  class="fixed bottom-0 py-8 grid place-items-center gap-8 w-full z-50"
>
  {#if isOpen}
    {#key key}
      <div
        class="mx-auto backdrop-blur-lg bg-white/40 w-fit py-1 px-3 md:py-2 md:px-6 rounded-full font-semibold uppercase shadow"
      >
        <nav
          in:slide={{ duration, delay: duration }}
          out:slide={{ duration }}
          aria-label="Main Menu"
        >
          <ul class="flex gap-1 md:gap-6 group text-xs md:text-base">
            <li>
              <a
                href="/articles"
                class="flex items-center gap-1 px-2 py-1 rounded-full md:hover:bg-black/10"
              >
                <div
                  class="border border-black rounded-full h-3 w-3"
                />
                <span>Articles</span>
              </a>
            </li>
            <li>
              <a
                href="/resources"
                class="flex items-center gap-1 px-2 py-1 rounded-full md:hover:bg-black/10"
              >
                <div
                  class="border border-black rounded-full h-3 w-3"
                />
                <span>Resources</span>
              </a>
            </li>
            <li>
              <a
                href="/contact"
                class="flex items-center gap-1 px-2 py-1 rounded-full md:hover:bg-black/10"
              >
                <div
                  class="border border-black rounded-full h-3 w-3"
                />
                <span>Contact</span>
              </a>
            </li>
          </ul>
        </nav>
      </div>
    {/key}
  {/if}
  <div class="mx-auto flex items-center gap-8">
    <a
      href="/"
      class="h-12 grid place-items-center bg-brand-green w-fit py-2 px-6 rounded-full text-sm md:text-base font-semibold shadow hover:bg-brand-green/70 transition"
    >
      <Logo client:load />
    </a>
    <button
      on:click={toggleMenu}
      class="h-12 flex items-center text-sm md:text-base backdrop-blur-lg bg-white/40 w-fit py-2 px-6 rounded-full font-semibold uppercase shadow md:hover:bg-white/70 transition"
      aria-expanded={isOpen}
      aria-controls="main-menu"
    >
      <div bind:this={animationContainer} class="h-8 w-8" />
      <span>Menu</span>
    </button>
  </div>
</header>
