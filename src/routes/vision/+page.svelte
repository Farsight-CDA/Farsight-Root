<script lang="ts">
    import accessibility from "$lib/images/accessibility.svg";
    import price from "$lib/images/price.svg";
    import wallet from "$lib/images/wallet.svg";
    import leon from "$lib/images/leon.png";
    import empty from "$lib/images/empty.png";
    import Advantage from "./Advantage.svelte";
    import AboutUs from "./AboutUs.svelte";


</script>

<div class="mx-10  mt-3">
    <div class="flex flex-col items-center justify-center accent h-max p-2 rounded-2xl">
        <h1 class="font-bold text-5xl">Crypto addresses are UGLY!</h1>

        <div class="mt-3 text-center">
            <p>Yes they are functional and a must for crypto to work.</p>
            <p>But they are not pretty: You cannot remember, share or compare them easily.</p>
        </div>

    </div>

    <div class="flex items-center justify-center accent mt-3 h-max p-2 rounded-2xl">
        <h1 class="font-bold text-5xl">Why not choose an existing solution?</h1>
    </div>

    <ul class="grid auto-cols">
        <li class="p-3">
            <Advantage 
                image={accessibility} 
                title="Accessibility"
                description="No need to connect to a specific network or hold a specific token for payment."    
            />
        </li>
        <li class="p-3">
            <Advantage
                image={price}
                title="Price"
                description="A registration fee is a must for several reasons. But there is no need for high gas fees."    
            />
        </li>
        <li class="p-3">
            <Advantage 
                image={wallet}
                title="Tighter wallet support"
                description="Names and wallets have to be closely coupled. Everyone with a wallet should also have a name for that wallet!"
            />
        </li>
    </ul>

    <div class="flex items-center justify-center accent mt-3 h-max p-2 rounded-2xl">
        <h1 class="font-bold text-5xl">About us</h1>
    </div>

    <ul class="grid auto-cols">
        <li class="p-3">
            <AboutUs
                    image={leon}
                    title="Leon"
                    description="I'm 23 years old. Currently I'm still studying computer science at the Technical University of Darmstadt. Although I have been writing software for 3 years, my crypto journey started only at the beginning of 2021. I am working full time on waiver since october 2022"
            />
        </li>
        <li class="p-3">
            <AboutUs
                    image={empty}
                    title="Elias"
                    description="Names and wallets have to be closely coupled. Everyone with a wallet should also have a name for that wallet!"
            />
        </li>
    </ul>
</div>


<style>
    .auto-cols {
        grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
    }
</style>