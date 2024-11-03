<!-- src/Modal.svelte -->
<script lang="ts">
  import { createBubbler, stopPropagation } from 'svelte/legacy';

  const bubble = createBubbler();
	import InfiniteScroll from "./infinite_scroll.svelte";

  interface Props {
    isOpen?: boolean;
    onClose?: any;
  }

  let { isOpen = false, onClose = () => {} }: Props = $props();
</script>

{#if isOpen}
  <div class="fixed inset-0 bg-black bg-opacity-50 flex items-center justify-center z-50" onclick={onClose} role="button" tabindex="0">
    <div
      class="bg-white rounded-lg shadow-lg max-w-md w-full p-6 relative"
      onclick={stopPropagation(bubble('click'))}
    >
      <h2 class="text-xl font-bold mb-4">Infinite Scroll Modal</h2>
      <p class="mb-4">Scroll down to load more items:</p>

      <!-- Infinite Scroll Component -->
      <InfiniteScroll />

      <button
        class="bg-blue-500 hover:bg-blue-600 text-white px-4 py-2 rounded mt-4"
        onclick={onClose}
      >
        Close
      </button>
    </div>
  </div>
{/if}
