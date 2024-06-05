<script lang="ts">
  import Toolbar from "$lib/components/toolbar.svelte";
  import Letter from "$lib/components/ui/letter.svelte";
  import { differenceInSeconds } from "date-fns";
  import { generate } from "random-words";

  let wordCount = 5;
  let randomWords = generate(wordCount);
  let start: Date | null = null;
  let end: Date | null = null;
  let wordState = [...(randomWords as string[]).join(" ")].map((letter) => {
    return {
      letter,
      state: "untyped",
    };
  });
  let currentWordIndex = 0;
  let lastIncorrectIndex = -1;

  function onKeyDown(e) {
    switch (e.keyCode) {
      case 32:
        checkCharacter(" ");
        break;
      case 65:
        checkCharacter("a");
        break;
      case 66:
        checkCharacter("b");
        break;
      case 67:
        checkCharacter("c");
        break;
      case 68:
        checkCharacter("d");
        break;
      case 69:
        checkCharacter("e");
        break;
      case 70:
        checkCharacter("f");
        break;
      case 71:
        checkCharacter("g");
        break;
      case 72:
        checkCharacter("h");
        break;
      case 73:
        checkCharacter("i");
        break;
      case 74:
        checkCharacter("j");
        break;
      case 75:
        checkCharacter("k");
        break;
      case 76:
        checkCharacter("l");
        break;
      case 77:
        checkCharacter("m");
        break;
      case 78:
        checkCharacter("n");
        break;
      case 79:
        checkCharacter("o");
        break;
      case 80:
        checkCharacter("p");
        break;
      case 81:
        checkCharacter("q");
        break;
      case 82:
        checkCharacter("r");
        break;
      case 83:
        checkCharacter("s");
        break;
      case 84:
        checkCharacter("t");
        break;
      case 85:
        checkCharacter("u");
        break;
      case 86:
        checkCharacter("v");
        break;
      case 87:
        checkCharacter("w");
        break;
      case 88:
        checkCharacter("x");
        break;
      case 89:
        checkCharacter("y");
        break;
      case 90:
        checkCharacter("z");
        break;
    }
  }

  function checkCharacter(char: string) {
    if (start === null) {
      start = new Date();
    }
    let state = "untyped";
    if (char === wordState[currentWordIndex].letter) {
      state = "correct";
      lastIncorrectIndex = -1;
    } else {
      if (lastIncorrectIndex !== -1) {
        return;
      }

      lastIncorrectIndex = currentWordIndex;
      state = "incorrect";
    }

    wordState = wordState.map((word, index) => {
      return index === currentWordIndex
        ? {
            ...word,
            state,
          }
        : word;
    });

    currentWordIndex += 1;

    if (currentWordIndex === wordState.length) {
      end = new Date();
    }
  }

  const wordsPerMinute = (): string => {
    const secondsDifference = differenceInSeconds(end!, start!);

    return ((wordCount / secondsDifference) * 60).toFixed(0);
  };

  const accuracy = (): string => {
    return (
      (wordState.filter((wordStateItem) => wordStateItem.state === "correct")
        .length /
        wordState.length) *
      100
    ).toFixed(2);
  };

  const reset = () => {
    randomWords = generate(wordCount);
    start = null;
    end = null;
    wordState = [...(randomWords as string[]).join(" ")].map((letter) => {
      return {
        letter,
        state: "untyped",
      };
    });
    currentWordIndex = 0;
    lastIncorrectIndex = -1;
  };
</script>

<section class="m-auto w-6/12 h-2/6">
  <Toolbar
    changeWordCount={(words) => {
      wordCount = words;
      reset();
    }}
    currentWordCount={wordCount}
  />
  {#if end}
    <div class="flex justify-center items-center mx-auto space-x-6 mb-10">
      <p class="text-2xl text-orange-500 font-black">WPM: {wordsPerMinute()}</p>
      <p class="text-2xl text-orange-500 font-black">Acc: {accuracy()}%</p>
    </div>
  {/if}
  <div class="flex flex-wrap mx-auto justify-center">
    {#each wordState as word}
      <Letter
        letter={word.letter}
        space={word.letter === " "}
        state={word.state}
      />
    {/each}
  </div>
</section>

<svelte:window on:keydown|preventDefault={onKeyDown} />
