<script>
    export let id
	const posts = JSON.parse(localStorage.getItem("posts"));
	const desiredPost = posts.find(post => post.id === id);
</script>

<div>
	<h3>{desiredPost.title}</h3>
	<p>{desiredPost.title}</p>
	<p>Дата создания: {desiredPost.createDate}</p>
	<p>Дата редактирования: {desiredPost.editDate}</p>
</div>
