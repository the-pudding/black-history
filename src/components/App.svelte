<script>
  import Quiz from "$components/Quiz.svelte";
  import Story from "$components/Story.svelte";
  import Footer from "$components/Footer.svelte";

  let quizFinished = false;
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

  <Quiz bind:isFinished={quizFinished} />

  {#if quizFinished}
    <Story />
    <p>Thanks for reading, hope you learned about someone new.</p>
  {/if}
</div>

<Footer />

<style>
  .container {
    width: 500px;
    margin: auto;
  }
</style>
