<script lang="ts">
  import { Route, Router } from "svelte-routing";
  import Library from "./Library/Library.svelte";
  import Detail from "./Detail/Detail.svelte";

  export let url = "";
</script>

<Router {url}>
  <main>
    <Route path="/">
      <Library />
    </Route>
    <Route let:params path="/albums/:id">
      <Detail id={params.id} />
    </Route>
  </main>
</Router>
