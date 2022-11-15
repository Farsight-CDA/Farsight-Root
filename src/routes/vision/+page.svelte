<script lang="ts">
    import accessibility from "$lib/images/accessibility.svg";
    import price from "$lib/images/price.svg";
    import wallet from "$lib/images/wallet.svg";
    import leon from "$lib/images/leon.png";
    import empty from "$lib/images/empty.png";
    import logo from '$lib/images/logo.png';

    import lookup from "$lib/images/lookup.png";

    import twitter from "$lib/images/platforms/twitter.svg"

    import Advantage from "./Advantage.svelte";
    import AboutUs from "./AboutUs.svelte";
	import CrossChainVisualization from "./CrossChainVisualization.svelte";

</script>

<svelte:head>
    <meta property="og:title" content="Farsight Names" />
    <meta property="og:type" content="website" />
    <meta property="og:url" content="https://farsight-names.de/vision" />
    <meta property="og:image" content="https://farsight-names.de{logo}" />
    <meta property="og:description" content="We want to make Web3 more accessible for everyone, let us sunset the days of cryptic addresses!" />
    <meta name="theme-color" content="#FF0000">
</svelte:head>

<div class="mt-3 relative">

    <a  class="w-12 absolute top-5 right-5"
        href="https://twitter.com/FarsightNames" target="_blank" rel="noreferrer">
        <img src={twitter} alt=""/>
    </a>

    <div class="flex flex-col justify-between items-center">
            <h1 class="font-bold text-5xl">Farsight - Names</h1>
            <p class="text-xl mt-2">A cross-chain aware address labelling service</p>
    </div>

    <div class="rounded-2xl p-4">
        <h2 class="font-bold text-3xl mb-2">The future of crypto is cross-chain</h2>
        <hr class="my-3">
        <div class="grid auto-cols-600">
            <div class="pr-16 flex flex-col justify-around p-3">
                <p>
                    Every week we see new blockchains, protocols appear in the space.
                    For some people all those new technologies are exciting, but the majority of users will only ever touch a small subset of all blockchains.
                </p>
                <br>
                <h3 class="font-bold text-lg">We see a few issues that arise from having so many blockchains:</h3>
                <ul class="pl-6 list-disc">
                    <li>
                        Each chain comes with its own set of software
                        => Wallets, DApps, ...
                    </li>
                    <li>
                        Uncertainty around addresses
                        => Which blockchain does each address belong to?
                    </li>
                    <li>
                        Difficulty to understand the matter for less experienced users
                    </li>
                    <li>
                        Accepting / Sending payments always requires negotiating a payment network
                    </li>
                </ul>

                <br>

                <h3 class="font-bold text-lg">We are competing with a system that is way simpler and more user friendly!</h3>
                <p>
                    It is time to bring all the tech that was built in crypto over the last years to use!
                    We need accessibility and ease of access. No compromises.
                </p> 
            </div>
            <div class="border border-solid m-2 rounded-xl">
                <CrossChainVisualization></CrossChainVisualization>
            </div>
        </div>
    </div>

    <div class="flex items-center justify-center accent mt-3 h-max p-2">
        <h1 class="font-bold text-5xl">Why address labels?</h1>
    </div>

    <div class="grid auto-cols-600">
        <img class="p-3 w-full" src={lookup} alt="">    
        <div class="p-3 flex flex-col justify-around">
            <div>
                <h3 class="text-xl font-bold">Addresses are UGLY!</h3>
                <p>
                    Yes, they really are. <br>
                    But that is not what makes them unsuitable for a lot of people.
                    Current financial services use information that is easy to compare, verify and share.
                    Data like an email address or even just the full name. They are easy to work with and its hard to make a mistake using them.
                    There is a reason why bank transfers, that still require klunky numbers are declining in popularity.

                    People will not go back to a system that is less comfortable than what they are currently used to.
                </p>
            </div>

            <br>

            <div>
                <h3 class="text-xl font-bold">How do address labels fit into the picture?</h3>
                <p>
                    Address labels try to abstract away the underlying address and network as much as possible. 
                    Instead of using many addresses across chains there has to be just a single name. 
                    This name should not be bound to any specific blockchain or address but instead be smoothly accessable and usable from anywhere.
                    It's not the task of a name system to decide which chains users are able to work with easily. 
                </p>
            </div>
        </div>
    </div>

    <div class="flex items-center justify-center accent mt-3 h-max p-2">
        <h1 class="font-bold text-5xl">Why not choose an existing solution?</h1>
    </div>

    <ul class="grid auto-cols-250">
        <li class="p-3">
            <Advantage
                image={price}
                title="Price"
            >
                <p>A registration fee is a must for several reasons.</p>
                <p>But in order to target especially new users there has to be a free tier that can be used gas free without any knowledge of the system.</p>
            </Advantage>
        </li>
        <li class="p-3">
            <Advantage 
                image={accessibility} 
                title="Accessibility"    
            >
                <p>
                    If registering a name requires you to connect to a specific blockchain or hold a specific token / coin the target group shrinks by a lot.
                    A name system shouldn't have opinions about which chain to support.
                </p>
            </Advantage>
        </li>
        <li class="p-3">
            <Advantage 
                image={wallet}
                title="Tighter wallet support"
            >
                <p>Names and wallets have to be closely coupled. Everyone with a wallet should also have a name for that wallet!</p>
                <p>Ideally a name registration should be included in the wallet creation process</p>
            </Advantage>
        </li>
    </ul>

    <div class="flex items-center justify-center accent mt-3 h-max p-2">
        <h1 class="font-bold text-5xl">About us</h1>
    </div>

    <ul class="grid auto-cols-350">
        <li class="p-3">
            <AboutUs
                    image={leon}
                    name="Leon Wenderoth (23)"
                    twitterHandle="LeonMalteW"
            >
                Currently I'm still studying computer science at the Technical University of Darmstadt. Although I have been writing software for 3 years, my crypto journey started only at the beginning of 2021. I am working full time on Farsight since october 2022
            </AboutUs>
        </li>
        <li class="p-3">
            <AboutUs
                    image={empty}
                    name="Elias Wolf (21)"
                    twitterHandle="Playwo_"
            >
                <div>
                    <p>
                        Computer Science Undergraduate at the technical university Darmstadt.
                    </p>
   
                </div>

                5 years experience in software development | 3 years experience in crypto.
                
                <p>
                    Implementation of a mining pool software for <a href="https://www.teepool.com/">Teepool</a> |
                    Passionate blockchain analyst via <a href="https://flipsidecrypto.xyz/Playwo">FlipsideCrypto</a> |
                    Flipside <a href="https://flipsidecrypto.xyz/buildathon">Build-A-Thon</a> category winner team leader.
                </p>
            </AboutUs>
        </li>
    </ul>
</div>


<style>
    .auto-cols-250 {
        grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
    }
    .auto-cols-350 {
        grid-template-columns: repeat(auto-fit, minmax(350px, 1fr));
    }
    .auto-cols-600 {
        grid-template-columns: repeat(auto-fit, minmax(min(600px, 100%), 1fr));
    }

    a {
        color: var(--link-color);
    }
</style>