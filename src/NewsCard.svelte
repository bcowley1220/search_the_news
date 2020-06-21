<script>
	import {onMount} from 'svelte';
	// import searchNews from './SearchHeader.svelte';
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
						`http://newsapi.org/v2/top-headlines?` +
						'country=us&' +
						'apiKey=24036c93ea52469a83075629f87a04b1');
			json = await response.json();
			console.log(json)
			articles = json.articles;
			console.log(articles)
		}
	);
	
	let searchRequest = async () => {
			json = null;
			response = await fetch(`http://newsapi.org/v2/everything?q=${newsStories}&apiKey=24036c93ea52469a83075629f87a04b1`);
			console.log(json);
			json = await response.json();
			console.log('before articles', json);
			articles = json.articles;
		}


</script>

<style>

		#cardContainer {
			display: flex;
			padding: .75em;
			height: 100vh;
			max-width: 100%;
			flex-flow: row wrap;
			justify-content: center;
			align-items: center;
		}
		.newsCardWrapper {
			height: 300px;
			min-height: 35vh;
			max-height: 35vh;
			width: 100%;
			min-width: 350px;
			max-width: 350px;
			margin: 1em;
		}
	.newsCard {
		height: 100%;
	}
	.newsCard, .newsCard_header, .newsCard_content, #cardContainer{
		display: flex;
	}
	.newsCard_header {
		border: solid 1px lightgrey;
		border-radius: 5px 5px 0px 0px;
		background: #fff;
	}
	.newsCard {
		height: 100%;
		flex-flow: column nowrap;
		max-height: 100%;
	}
	.newsCard_header, .newsCard_content {
		padding: 1em;
		justify-content: center;
		align-items: center;
	}
	.newsCard_content {
		height: 81%;
		padding: 0;
	}
	img {
		object-fit: fill;
		border-radius: 0px 0px 5px 5px;
	}
		.newsCard_content>a, a>img {
				max-height: 100%;
		}

	.newsCard_header {
		font-size: 12px;
		height: 10%;
	}
	.searchWrapper, .searchWrapper>label {
		display: flex;
		flex-flow: column wrap;
		justify-content: center;
		align-items: center;
	}
	h1, h2 {
		text-align: center;
		margin: 1em;
	}
	#newsSearch {
    padding: .5em;
    border-radius: 4px;
    border: solid 1px lightgray;
    margin-bottom: 1em;
	}
	button {
    padding: .5em;
    width: 5em;
    border-radius: 4px;
    border: unset;
		background: lightblue;
		transition: background .5s ease, color .25s ease;
	}
	button:hover{
		background: darkslateblue;
		color: #fff;
	}

</style>
<h1>Search Top Stories </h1>
<form class='searchWrapper'>
	<label for="newsSearch">
		<input id='newsSearch' type="text"  bind:value={newsStories} placeholder="Coronavirus">
	</label>
	<button type="button" on:click={searchRequest}>Search</button>
</form>
<h2>
	{newsStories} Headlines
</h2>
<section id='cardContainer'>

</section>
