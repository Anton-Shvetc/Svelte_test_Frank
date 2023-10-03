<!-- App.svelte -->
<script>
  import { Router, Link, Route } from "svelte-routing";
  import Home from "./routes/Home.svelte";
  import Post from "./routes/Post.svelte";
  import FormPost from "./routes/FormPost.svelte";
  export let url = "";
</script>

<Router {url}>
  <nav>
    <Link to="/">Главная</Link>
	  <Link to="/create">Добавить</Link>
  </nav>
	<Route path="/create" component={FormPost} />
  <Route path="/" component={Home} />
  <Route path="/:id" let:params> <Post id={params.id} /></Route>
  <Route path="/edit/:id" let:params> <FormPost id={params.id}/></Route>
</Router>
