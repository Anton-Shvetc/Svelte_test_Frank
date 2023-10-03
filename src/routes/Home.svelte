<script>
  import { onMount } from 'svelte';
  import { Link } from "svelte-routing";

  let posts = [];

  onMount(() => {
    const storedPosts = localStorage.getItem('posts');
    if (storedPosts) {
      posts = JSON.parse(storedPosts);
    } else {
      posts = [];
    }
  });

</script>

<main>
  {#if posts.length === 0}
    <p>Нет сохраненных постов.</p>
  {:else}
    {#each posts as post (post.id)} 
    <div class="post">
      <h3>{post.title}</h3>
      <p>Дата создания: {post.createDate}</p>
      <p>{post.editDate ? `Дата редактирования: ${post.editDate}` : ""} </p>
      <Link to={`/${post.id}`}>  Подробнее  </Link>  
      <Link to={`/edit/${post.id}`}>  Редактировать  </Link>  
    </div>
    {/each}
  {/if}
</main>

<style>
  .post {
    margin-bottom: 20px;
    padding: 10px;
    border: 1px solid #ccc;
    border-radius: 4px;
  }
</style>