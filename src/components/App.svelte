<script>
  import Quiz from "$components/Quiz.svelte";
  import Story from "$components/Story.svelte";
  import Footer from "$components/Footer.svelte";

  let quizFinished = false;
  let user = null;
</script>

<div class="container">
  <p>
    It's Black History Month (or at least it was when this was published)! We're going to see how
    many famous Black Americans you know.
  </p>
  <p>
    We'll show you a name, see if you recognize it, and then if you can answer a basic question
    about them.
  </p>

  <div class="personalize">
    <p>Who are you? (so i can do some fake personalization)</p>
    <button on:click={() => (user = "matt")}>Matt</button>
    <button on:click={() => (user = "russell")}>Russell</button>
    <button on:click={() => (user = "rob")}>Rob</button>
    <button on:click={() => (user = "michelle")}>Michelle</button>
    {#if user}<p>thank you!</p>{/if}
  </div>

  <Quiz bind:isFinished={quizFinished} />

  {#if quizFinished}
    <Story {user} />
    <p>Thanks for reading, hope you learned about someone new.</p>
  {/if}
</div>

<Footer />

<style>
  button {
    background: lightblue;
  }
  .personalize {
    margin-bottom: 1.5em;
  }
  .container {
    width: 500px;
    margin: auto;
  }
</style>
