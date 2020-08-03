<script>
  export let article;
</script>

<div class="newsCardWrapper">
  <article class="newsCard">
    <header class="newsCard_header">{article.title}</header>
    <div class="newsCard_content">
      <a href={article.url}>
        <img
          src={article.urlToImage}
          alt="Link To Story Image: {article.urlToImage}"
          height="243"
          width="350" />
      </a>
    </div>
  </article>
</div>
