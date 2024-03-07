<script>
    import ProductInfo from "./ProductInfo.svelte";
    let details = [
        {id:0, src: "https://m.media-amazon.com/images/I/61zaC+-OF+L.jpg", name: "Women's Cargo Utility Jogger", price: 78.00, desc: "Size, Medium Color: Black", quantity: 3},
        {id:1, src: "https://m.media-amazon.com/images/I/61zaC+-OF+L.jpg", name: "Women's Cargo Utility Jogger", price: 780.00, desc: "Size, Medium Color: Black", quantity: 3},
        {id:2, src: "https://m.media-amazon.com/images/I/61zaC+-OF+L.jpg", name: "Women's Cargo Utility Jogger", price: 8.00, desc: "Size, Medium Color: Black", quantity: 3},
        {id:3, src: "https://m.media-amazon.com/images/I/61zaC+-OF+L.jpg", name: "Women's Cargo Utility Jogger", price: 230.00, desc: "Size, Medium Color: Black", quantity: 3},
        {id:4, src: "https://m.media-amazon.com/images/I/61zaC+-OF+L.jpg", name: "Women's Cargo Utility Jogger", price: 38.00, desc: "Size, Medium Color: Black", quantity: 3},
        {id:5, src: "https://m.media-amazon.com/images/I/61zaC+-OF+L.jpg", name: "Women's Cargo Utility Jogger", price: 4800.00, desc: "Size, Medium Color: Black", quantity: 3}
    ]
    const updateQuantity = (e) => {
        console.log(e.detail)
        for(var i = 0; i < details.length; i++){
            if(details[i].id === e.detail.id){
                details[i] = e.detail;
                break
            }
        }
    }

    const removeItem = (e) => {
        for(var i = 0; i < details.length; i++){
            if(details[i].id === e.detail.id){
                const index = details.indexOf(details[i])
                details.splice(index, 1);
                details = details
                break
            }
        }
    }

    $: subtotal = details.reduce((a, b)=>a + b.price*b.quantity,0)
    $: fee = parseFloat((subtotal * 0.005).toFixed(2));
    $: total = subtotal + fee;
</script>

<div class="w-[98vw] overflow-y-scroll remove-scrollbar md:w-[80vw]">
    <h1 class="font-bold text-xl md:text-2xl">Checkout</h1> 
    {#if details.length > 0}
        {#each details as detail (detail.id)}
            <ProductInfo {detail} on:updateQuantity={updateQuantity} on:removeItem={removeItem} />
        {/each}
        <div class="mt-4">
        <div class="flex my-4 justify-between">
            <h2 class="font-normal text-xm text-gray-500 md:text-xl">Subtotal</h2>
            <h2 class="font-normal text-xm md:text-xl">${subtotal}</h2>
        </div>
        <div class="flex my-4 justify-between">
            <h2 class="font-normal text-xm text-gray-500 md:text-xl">Estimated Shipping Fee</h2>
            <h2 class="font-normal text-xm md:text-xl">${fee}</h2>
        </div>
        <div class="flex my-4 justify-between">
            <h2 class="font-normal text-xm text-gray-500 md:text-xl">Estimated Tax</h2>
            <h2 class="font-normal text-xm md:text-xl">To be determined</h2>
        </div>
        <div class="flex my-4 justify-between">
            <h2 class="font-normal text-xm text-gray-500 md:text-xl">Total</h2>
            <h2 class="font-normal text-xm md:text-xl">${total}</h2>
        </div>
        <div class="flex justify-center">
            <button class="text-white bg-blue-700 p-2 rounded-lg w-[40vw] font-semibold mt-2">Secure Checkout</button>
        </div>
        </div>
    {:else}
        <div class="flex h-[85vh] justify-center items-center text-gray-300 text-3xl">No item in the cart</div>
    {/if}
</div>