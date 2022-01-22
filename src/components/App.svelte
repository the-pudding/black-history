<script>
  import Quiz from "$components/Quiz.svelte";
  import Story from "$components/Story.svelte";
  import Footer from "$components/Footer.svelte";
  import classics from "$data/classics.csv";
  import locals from "$data/locals.csv";

  let quiz1Finished = false;
  let quiz2Finished = false;
  let user = null;
</script>

<div class="container">
  <h1>Black history, but in your own backyard</h1>
  <p>It's Black History Month! Let's see which Black historical figures you recognize.</p>

  <Quiz bind:isFinished={quiz1Finished} data={classics} />

  {#if quiz1Finished}
    <p>
      Readers of this piece have gotten <strong>90%</strong> of questions about these classic figures
      correct.
    </p>
    <p>
      Not surprising because these are people we talk about a lot. In a
      <a href="https://journals.sagepub.com/doi/full/10.1177/2332858420940312">study</a> that looked
      at widely used textbooks in Texas, they found these were the top mentioned Black people.
    </p>
    <details>
      <summary>Why Texas?</summary>
      Texas has the 2nd largest student population in the U.S. Since it's such a big textbook market,
      it's actually
      <a
        href="https://www.washingtonpost.com/outlook/2020/10/19/conservative-activists-texas-have-shaped-history-all-american-children-learn/"
        >influential</a
      > on all U.S. textbooks.
    </details>

    <p>[chart of people by # of mentions]</p>

    <p>Ok, see if you recognize these people.</p>

    <!-- <div class="personalize">
    <p>Who are you? (so i can do some fake personalization)</p>
    <button on:click={() => (user = "matt")}>Matt</button>
    <button on:click={() => (user = "russell")}>Russell</button>
    <button on:click={() => (user = "rob")}>Rob</button>
    <button on:click={() => (user = "michelle")}>Michelle</button>
    {#if user}<p>thank you!</p>{/if}
  </div> -->

    <Quiz bind:isFinished={quiz2Finished} data={locals} />

    {#if quiz2Finished}
      <p>
        Those were all people who were born, lived, or did something important near where you are,
        in <strong>Oakland, California.</strong>.
      </p>
      <p>
        Readers have goten <strong>42%</strong> of questions about people local to them correct.
      </p>
      <h3>Black history within 100 miles of Oakland, California</h3>
      <p>[big explorable map, ideas below]</p>

      <img src="assets/maps.png" />

      <button>Do this again, but from a new place!</button>
    {/if}
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
  img {
    margin-bottom: 1em;
  }
  details {
    font-size: 0.75rem;
  }
</style>
