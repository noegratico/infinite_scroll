<!-- src/InfiniteScroll.svelte -->
<script  lang="ts">
    import { onMount } from 'svelte';
    let posts:any[] = $state([]);
    let loading = $state(false);
    let page = 1;
  
    // Function to fetch data from JSONPlaceholder
    async function loadMore() {
      if (loading) return;
      loading = true;
  
      try {
        const response = await fetch(`https://jsonplaceholder.typicode.com/posts?_limit=10&_page=${page}`);
        const newPosts = await response.json();
        
        // Append new posts to the list
        posts = [...posts, ...newPosts];
        page++;
      } catch (error) {
        console.error("Failed to load posts:", error);
      } finally {
        loading = false;
      }
    }
  
    // Load initial data on component mount
    onMount(loadMore);
  
    // Handle scroll event to trigger loadMore
    function handleScroll(event:any) {
      const { scrollTop, scrollHeight, clientHeight } = event.target;
      if (scrollTop + clientHeight >= scrollHeight - 20) {
        loadMore();
      }
    }
  </script>
  
  <div
    onscroll={handleScroll}
    class="overflow-y-auto max-h-80 border p-4"
  >
    <ul class="space-y-4">
      {#each posts as post}
        <li class="bg-gray-100 p-4 rounded shadow">
          <h3 class="font-bold">{post.title}</h3>
          <p>{post.body}</p>
        </li>
      {/each}
    </ul>
  
    {#if loading}
      <p class="text-center text-gray-500 mt-4">Loading...</p>
    {/if}
  </div>
  
  <style>
    /* Ensure the div can scroll */
    .overflow-y-auto {
      scrollbar-width: thin;
    }
  </style>
  