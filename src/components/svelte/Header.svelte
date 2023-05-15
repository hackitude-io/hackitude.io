<script>
  import { slide } from 'svelte/transition';

  let key;
  let duration;

  let isOpen = false;
</script>

<header class="fixed bottom-0 py-8 grid place-items-center gap-8 w-full">
  {#if isOpen}
  {#key key}
    <nav
    in:slide={{ duration, delay: duration }}
    out:slide={{ duration }}
    class="mx-auto backdrop-blur-lg bg-white/40 w-fit py-2 px-6 rounded-full font-semibold uppercase shadow">
      <ul class="flex gap-6">
        <li>
          <a href="#" class="flex items-center gap-1 px-2 py-1 rounded-full hover:bg-black/10">
            <div class="border border-black rounded-full h-3 w-3"/>
            <span>Work</span>
        </a>
        </li>
        <li>
          <a href="#" class="flex items-center gap-1 px-2 py-1 rounded-full hover:bg-black/10">
            <div class="border border-black rounded-full h-3 w-3"/>
            <span>Articles</span>
        </a>
        </li>
        <li>
          <a href="#" class="flex items-center gap-1 px-2 py-1 rounded-full hover:bg-black/10">
            <div class="border border-black rounded-full h-3 w-3"/>
            <span>Contact</span>
          </a>
        </li>
      </ul>
    </nav>
    {/key}
  {/if}
  <div class="mx-auto flex gap-8">
    <a href="/" class="bg-brand-green w-fit py-2 px-6 rounded-full font-semibold shadow">hackitude.io</a>
    <button
    on:click={() => isOpen = !isOpen}
    class="backdrop-blur-lg bg-white/40 w-fit py-2 px-6 rounded-full font-semibold uppercase shadow">
    <span>Menu</span>
    </button>
</div>
</header>