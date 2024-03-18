<script>
  import MdRemove from "svelte-icons/md/MdRemove.svelte";
  import MdAdd from "svelte-icons/md/MdAdd.svelte";
  import MdDelete from "svelte-icons/md/MdDelete.svelte";
  import { createEventDispatcher } from "svelte";
  export let detail;

  $: src = detail.src;
  $: name = detail.name;
  $: price = detail.price;
  $: desc = detail.desc;
  $: quantity = detail.quantity;

  const dispatch = createEventDispatcher();
  let handleQty = (add) => {
    if (add) {
      detail = { ...detail, quantity: ++quantity };
    } else {
      detail = { ...detail, quantity: --quantity };
    }
    dispatch("updateQuantity", detail);
  };

  let handleRemove = () => dispatch("removeItem", detail);
</script>

<div class="flex my-4 items-center">
  <div class="overflow-hidden h-[12vh] w-20 md:h-20 rounded-lg">
    <img {src} alt="" class="h-full w-full" />
  </div>
  <div class="ml-4 w-full">
    <div class="flex justify-between">
      <h2 class="font-semibold text-xm md:text-xl">{name}</h2>
      <button class="w-5 mr-3 md:w-6" on:click={() => handleRemove()}
        ><MdDelete /></button
      >
    </div>
    <h2 class="font-normal text-sm text-gray-500 md:text-xm">{desc}</h2>
    <div class="flex justify-between w-full">
      <h2 class="font-normal text-sm text-gray-500 md:text-xm">${price}</h2>
      <div class="flex px-3">
        <button
          disabled={quantity === 1}
          class="flex items-center px-1 text-sm border-2 border-gray-300"
          on:click={() => handleQty(false)}
        >
          <span class="w-4"><MdRemove /></span>
        </button>
        <span class="px-2 font-semibold text-xm border-y-2 border-gray-300"
          >{quantity}</span
        >
        <button
          disabled={quantity === 100}
          class="flex items-center px-1 border-2 border-gray-300"
          on:click={() => handleQty(true)}
        >
          <span class="w-4"><MdAdd /></span>
        </button>
      </div>
    </div>
  </div>
</div>
