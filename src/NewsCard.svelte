<script>
  import { onMount } from "svelte";
  import Card from "./Card.svelte";
  window.process = { env: 'development' }
  let newsSearch;
  let articles = [];
  let request;
  let response;
  let json;
  let cardCounter = 0;
  let newsStories = "";

  const keepItSecret = KEEP_IT_SECRET;

  console.log(process.env.NODE_ENV);
  onMount(
    (request = async () => {
      json = null;
      response = await fetch(
        `https://newsapi.org/v2/top-headlines?` +
          "country=us&" +
          `apiKey=${keepItSecret}`
      );
      json = await response.json();
      console.log(json);
      articles = json.articles;
    })
  );

  let searchRequest = async () => {
    json = null;
    response = await fetch(
      `http://newsapi.org/v2/everything?q=${newsStories}&apiKey=${keepItSecret}`
    );
    json = await response.json();
    articles = json.articles;
  };
</script>

<h1>Search Top Stories</h1>
<div class="inputWrapper">
  <label for="newsSearch">
    <input
      id="newsSearch"
      type="text"
      bind:value={newsStories}
      placeholder="Coronavirus" />
  </label>
  <button type="button" on:click={searchRequest}>Search</button>
</div>
<h2>{newsStories} Headlines</h2>
<section id="cardContainer">
  {#each articles as article}
    <Card {article} />
  {/each}
</section>
