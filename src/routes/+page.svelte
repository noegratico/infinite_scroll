<!-- src/App.svelte -->
<script>
	import Modal from "$lib/components/Modal.svelte";

    let showModal = $state(false);
  
    function toggleModal() {
      showModal = !showModal;
    }
  </script>
  
  <div class="flex items-center justify-center min-h-screen bg-gray-100">
    <button
      class="bg-blue-500 hover:bg-blue-600 text-white px-6 py-3 rounded"
      onclick={toggleModal}
    >
      Open Modal
    </button>
  
    <Modal isOpen={showModal} onClose={toggleModal} />
  </div>
  