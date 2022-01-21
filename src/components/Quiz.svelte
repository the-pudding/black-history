<script>
  import _ from "lodash";
  import questions from "$data/questions.csv";

  export let isFinished;

  let isStarted = false;
  let stage = 0; // stage 0: recognition, stage 1: multiple choice, stage 2: next
  let index = 0;
  let results = [];
  let randomizedQuestions = _.shuffle(questions);
  $: ({ name, question, answerA, answerB, answerC } = randomizedQuestions[index]);
  $: answerOptions = _.shuffle([answerA, answerB, answerC]);
  let currentMultipleChoiceResult = false;

  const logRecognition = (response) => {
    results = [...results, { name, recognized: response }];
    if (response) {
      stage = 1;
    } else {
      advance();
    }
  };
  const logMultipleChoice = (e) => {
    const correctAnswer = answerA;
    const existingEntry = results.filter((d) => d.name === name)[0];

    results = [
      ...results.filter((d) => d.name !== name),
      { ...existingEntry, multipleChoice: e.target.innerText === correctAnswer }
    ];

    currentMultipleChoiceResult = e.target.innerText === correctAnswer;
    stage = 2;
  };
  const advance = () => {
    index += 1;
    console.log({ index });
    if (index >= questions.length) {
      isFinished = true;
      index = 0;
    } else {
      stage = 0;
    }
  };

  $: console.log({ results });
</script>

{#if isFinished}
  <br />
{:else if isStarted}
  <div>
    <p>{index + 1}/{questions.length}: Do you know who this is?</p>
    <p class="name"><strong>{name}</strong></p>
    <button on:click={() => logRecognition(true)} disabled={stage > 0}>👍🏾</button>
    <button on:click={() => logRecognition(false)} disabled={stage > 0}>👎🏾</button>
  </div>

  {#if stage > 0}
    <div>
      <p>{question}?</p>
      {#each answerOptions as option}
        <button on:click={logMultipleChoice} disabled={stage > 1}>{option}</button>
      {/each}
      {#if stage === 2}
        <div class="results">
          <p>{currentMultipleChoiceResult ? "correct! 🎉" : "incorrect ❌"}</p>
          <button on:click={advance}>next</button>
        </div>
      {/if}
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
  .results {
    display: flex;
    justify-content: space-between;
    width: 150px;
    height: 36px;
    align-items: center;
    margin-top: 1.5em;
  }
</style>
