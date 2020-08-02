<script>
<<<<<<< HEAD
	import {onMount} from 'svelte';
	let newsSearch;
	let articles = [];
	let request;
	let response;
	let json;
	let cardCounter = 0;
	let newsStories = '';
	
	onMount( 
		request = async () => {
			json = null;
			response = await fetch(
						`http://cors-anywhere.herokuapp.com/http://newsapi.org/v2/top-headlines?` +
						'country=us&' +
						'apiKey=24036c93ea52469a83075629f87a04b1');
			json = await response.json();
			console.log(json)
			return articles = json.articles;
			console.log(articles)
		}
	);
	
	let searchRequest = async () => {
			json = null;
			response = await fetch(`http://newsapi.org/v2/everything?q=${newsStories}&apiKey=24036c93ea52469a83075629f87a04b1`);
			console.log(json);
			json = await response.json();
			console.log('before articles', json);
			return articles = json.articles;
		}
=======
  import { onMount } from "svelte";
  import Card from "./Card.svelte";
  let newsSearch;
  let articles = [];
  let request;
  let response;
  let json;
  let cardCounter = 0;
  let newsStories = "";
>>>>>>> 17c6419f6f278d062ec9c379bf93df551ccee399

  onMount(
    (request = async () => {
      json = null;
      response = await fetch(
        `http://newsapi.org/v2/top-headlines?` +
          "country=us&" +
          "apiKey=24036c93ea52469a83075629f87a04b1"
      );
      json = await response.json();
      console.log(json);
      articles = json.articles;
    })
  );

  let searchRequest = async () => {
    json = null;
    response = await fetch(
      `http://newsapi.org/v2/everything?q=${newsStories}&apiKey=24036c93ea52469a83075629f87a04b1`
    );
    json = await response.json();
    articles = json.articles;
  };
</script>

<h1>Search Top Stories</h1>
<label for="newsSearch">
  <input
    id="newsSearch"
    type="text"
    bind:value={newsStories}
    placeholder="Coronavirus" />
</label>
<button type="button" on:click={searchRequest}>Search</button>
<h2>{newsStories} Headlines</h2>
<section id="cardContainer">
  {#each articles as article}
    <Card {article} />
  {/each}
</section>
