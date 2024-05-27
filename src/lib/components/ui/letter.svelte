<script lang="ts">
  import { twMerge } from "tailwind-merge";

  export let letter: string = "";
  export let space: boolean | null = null;
  export let state: "untyped" | "correct" | "incorrect" = "untyped";
</script>

<span
  class={twMerge(
    "m-0 h-auto flex-grow-0whitespace-nowrap",
    state === "incorrect"
      ? "text-red-500"
      : state === "correct"
        ? "text-green-500"
        : "text-white",
  )}
>
  {#if space}
    <span class="mx-1">.</span>
  {:else}
    {letter}
  {/if}
</span>
