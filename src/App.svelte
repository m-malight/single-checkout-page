<script>
  import Checkout from "./lib/Checkout.svelte";
  import Nav from "./lib/Nav.svelte";
</script>

<main>
  <div class="h-[7vh]">
    <Nav />
  </div>
  <div
    class="h-[91vh] flex justify-center overflow-y-scroll remove-scrollbar border-t-2 pt-2 border-gray-300"
  >
    <Checkout />
  </div>
</main>
