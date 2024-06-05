<script lang="ts">
  import { twMerge } from "tailwind-merge";

  export let changeWordCount: (words: number) => void;
  export let currentWordCount: number;
</script>

<div
  class="absolute rounded-lg shadow-lg py-4 px-6 bg-slate-950 text-white/60 top-5 left-1/2 -translate-x-1/2 flex space-x-2"
>
  <button
    class={twMerge(
      "w-6 h-6 group flex justify-center items-center focus:text-white",
      currentWordCount === 5 ? "text-white" : "",
    )}
    on:click={() => changeWordCount(5)}
  >
    <span class="cursor-pointer group-hover:text-white">5</span>
  </button>
  <button
    class={twMerge(
      "w-6 h-6 group flex justify-center items-center focus:text-white",
      currentWordCount === 20 ? "text-white" : "",
    )}
    on:click={() => changeWordCount(20)}
  >
    <span class="cursor-pointer group-hover:text-white">20</span>
  </button>
  <button
    class={twMerge(
      "w-6 h-6 group flex justify-center items-center focus:text-white",
      currentWordCount === 30 ? "text-white" : "",
    )}
    on:click={() => changeWordCount(30)}
  >
    <span class="cursor-pointer group-hover:text-white">30</span>
  </button>
</div>
