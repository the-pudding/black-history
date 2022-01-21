<script>
  import allNames from "$data/allNames.csv";
</script>

<p>Sweet, good job.</p>
<p>
  There are certain Black American historical figures that lots of people know. They have prominent
  roles our story of American history.
</p>
<p>
  These are the Black people whose names appear in the top 15 textbooks in Texas, sized by the
  number of mentions.
</p>
<img src="assets/chart1.png" />
<p>
  For example, <a href="https://en.wikipedia.org/wiki/Martin_Luther_King_Jr."
    >Martin Luther King Jr.</a
  >
  is referenced a bunch, and <strong>99%</strong> of readers of this piece recognized him (including
  you!).
</p>
<p>Here's how reader recognition compares to with textbook mentions.</p>
<img src="assets/chart2.png" />
<div>[+ another one for knowledge, correct answering of multiple choice question]</div>
<p>
  There are so many people not named in any of those top 15 textbooks, but who did big things in
  American politics, activism, entertainment, etc.
</p>
<div class="scroll">
  {#each allNames as { name }}
    {name + " "}
  {/each}
</div>
<p>
  Like <a href="https://en.wikipedia.org/wiki/Claudette_Colvin">Claudette Colvin</a>, who only
  <strong>25%</strong> of readers knew.
</p>
<p>
  Or <a href="https://en.wikipedia.org/wiki/Huey_P._Newton">Huey P. Newton</a>, since you're in
  <strong>Oakland, California</strong> (he lived there). <strong>55%</strong> of readers recognized him.
</p>
<div>[maybe plot these lesser-known people on the same chart above]</div>
<div>[then you can explore it and hover over other people]</div>

<style>
  .scroll {
    height: 200px;
    overflow: scroll;
    background: lightgrey;
    padding: 1em 0.5em 1em 0.5em;
  }
</style>
