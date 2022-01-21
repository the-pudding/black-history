<script>
  import _ from "lodash";
  import questions from "$data/questions.csv";

  export let isFinished;

  let isStarted = false;
  let multipleChoice = false;
  let index = 0;
  let results = [];
  let randomizedQuestions = _.shuffle(questions);
  $: ({ name, question, answerA, answerB, answerC } = randomizedQuestions[index]);
  $: answerOptions = _.shuffle([answerA, answerB, answerC]);

  const logRecognition = (response) => {
    results = [...results, { name, recognized: response }];
    multipleChoice = true;
  };
  const logMultipleChoice = (e) => {
    const correctAnswer = answerA;
    const existingEntry = results.filter((d) => d.name === name)[0];

    results = [
      ...results.filter((d) => d.name !== name),
      { ...existingEntry, multipleChoice: e.target.innerText === correctAnswer }
    ];

    multipleChoice = false;
    index += 1;
    if (index >= questions.length - 1) isFinished = true;
  };

  $: console.log({ results });
</script>

{#if isFinished}
  <br />
{:else if isStarted}
  <div>
    <p>{index + 1}/{questions.length}: Do you know who this is?</p>
    <p class="name"><strong>{name}</strong></p>
    <button on:click={() => logRecognition(true)} disabled={multipleChoice}>👍🏾</button>
    <button on:click={() => logRecognition(false)} disabled={multipleChoice}>👎🏾</button>
  </div>

  {#if multipleChoice}
    <div>
      <p>{question}?</p>
      {#each answerOptions as option}
        <button on:click={logMultipleChoice}>{option}</button>
      {/each}
    </div>
  {/if}
{:else}
  <button on:click={() => (isStarted = true)}>Start quiz</button>
  <button on:click={() => (isFinished = true)}>Skip quiz</button>
{/if}

<style>
  button {
    background: lightgrey;
  }
  .name {
    font-size: 2em;
  }
</style>
