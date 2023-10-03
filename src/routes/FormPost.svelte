<script>
  export let id;

  const posts = JSON.parse(localStorage.getItem("posts"));
  let desiredPost = id ? posts.find((post) => post.id === id) : "";
  let title = desiredPost.title ? desiredPost.title : "";
  let text = desiredPost.text ? desiredPost.text : "";

  const dateOptions = {
    year: "numeric",
    month: "long",
    day: "numeric",
    timezone: "UTC",
    hour: "numeric",
    minute: "numeric",
    second: "numeric",
  };

  const savePost = () => {
    const newId =
      Date.now().toString(36) + Math.random().toString(36).substr(2);

    if (id) {
      let updatedItems = posts.filter((item) => item.id !== id);

      const post = {
        id: id,
        title,
        text,
        createDate: desiredPost.createDate,
        // @ts-ignore
        editDate: new Date().toLocaleString("ru", dateOptions),
      };
      updatedItems.push(post);

      localStorage.setItem("posts", JSON.stringify(updatedItems));
    } else {
      const post = {
        id: newId,
        title,
        text,
        // @ts-ignore
        createDate: new Date().toLocaleString("ru", dateOptions),
        editDate: "",
      };
      let oldItems = JSON.parse(localStorage.getItem("posts")) || [];
      oldItems.push(post);
      localStorage.setItem("posts", JSON.stringify(oldItems));
    }

    alert("Данные обновлены");
    window.location.href = "/";
  };
</script>

<main>
  <h1>Добавить пост</h1>

  <form on:submit|preventDefault={savePost}>
    <div>
      <label for="title">Заголовок:</label>
      <input type="text" id="title" bind:value={title} required />
    </div>

    <div>
      <label for="text">Текст:</label>
      <textarea id="text" bind:value={text} required />
    </div>

    <button type="submit">Сохранить</button>
  </form>
</main>

<style>
  main {
    max-width: 600px;
    margin: 0 auto;
  }

  form > div {
    margin-bottom: 1rem;
  }

  label {
    font-weight: bold;
    display: block;
  }

  input,
  textarea {
    width: 100%;
    padding: 0.5rem;
    border: 1px solid #ccc;
    border-radius: 4px;
  }

  button {
    padding: 0.5rem 1rem;
    background-color: #007bff;
    color: #fff;
    border: none;
    border-radius: 4px;
    cursor: pointer;
  }
</style>
