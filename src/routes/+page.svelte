<script lang="ts">
  let posts: string[] = [];

  function calculate_posts() {
    const path_object = import.meta.glob("/src/lib/posts/*.svelte");
    posts = Object.keys(path_object).map(
      (path) => path.split("/").at(-1)?.replace(".svelte", "") ?? ""
    );
  }

  calculate_posts();
</script>

<svelte:head>
  <title>Posts</title>
</svelte:head>

<h1>Posts</h1>

<ul>
  {#each posts as post}
    <li>
      <a href="/post/{post}">{post}</a>
    </li>
  {/each}
</ul>
