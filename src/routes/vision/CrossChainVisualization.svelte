<script lang="ts">
import bitcoin_logo from "$lib/images/currencies/bitcoin.svg";
import ethereum_logo from "$lib/images/currencies/ethereum.svg";
import polkadot_logo from "$lib/images/currencies/polkadot.svg";
import cosmos_logo from "$lib/images/currencies/cosmos.svg";
import avalanche_logo from "$lib/images/currencies/avalanche.svg";
import flow_logo from "$lib/images/currencies/flow.svg";
import solana_logo from "$lib/images/currencies/solana.svg";

import { onMount } from "svelte";

export let lineThreshold: number = 0.45;
export let lineColor: string = "#f88a13";

let canvas: HTMLCanvasElement;
let container: HTMLDivElement;

onMount(() => {
    const ctx = canvas.getContext("2d")!;

    const icons: IconAnimationState[] = [];

    const bitcoin = new Image();
    bitcoin.src = bitcoin_logo;
    const ethereum = new Image();
    ethereum.src = ethereum_logo;
    const polkadot = new Image();
    polkadot.src = polkadot_logo;
    const cosmos = new Image();
    cosmos.src = cosmos_logo;
    const avalanche = new Image();
    avalanche.src = avalanche_logo;
    const flow = new Image();
    flow.src = flow_logo;
    const solana = new Image();
    solana.src = solana_logo;

    icons.push({
        image: bitcoin,
        posX: Math.random(),
        posY: Math.random(),
        incX: Math.random() > 0.5,
        incY: Math.random() > 0.5,
        speed: 1.3 * Math.random() / 1000
    });
    icons.push({
        image: ethereum,
        posX: Math.random(),
        posY: Math.random(),
        incX: Math.random() > 0.5,
        incY: Math.random() > 0.5,
        speed: 1.3 * Math.random() / 1000
    });
    icons.push({
        image: polkadot,
        posX: Math.random(),
        posY: Math.random(),
        incX: Math.random() > 0.5,
        incY: Math.random() > 0.5,
        speed: 1.3 * Math.random() / 1000
    });
    icons.push({
        image: cosmos,
        posX: Math.random(),
        posY: Math.random(),
        incX: Math.random() > 0.5,
        incY: Math.random() > 0.5,
        speed: 1.3 * Math.random() / 1000
    });
    icons.push({
        image: avalanche,
        posX: Math.random(),
        posY: Math.random(),
        incX: Math.random() > 0.5,
        incY: Math.random() > 0.5,
        speed: 1.3 * Math.random() / 1000
    });
        icons.push({
        image: flow,
        posX: Math.random(),
        posY: Math.random(),
        incX: Math.random() > 0.5,
        incY: Math.random() > 0.5,
        speed: 1.3 * Math.random() / 1000
    });
        icons.push({
        image: solana,
        posX: Math.random(),
        posY: Math.random(),
        incX: Math.random() > 0.5,
        incY: Math.random() > 0.5,
        speed: 1.3 * Math.random() / 1000
    });

    function draw() {
        const width = container.clientWidth;
        const height = container.clientHeight;

        canvas.width = width;
        canvas.height = height;

        const iconSize = Math.min(width / 8, height / 8);
        const xLimit = width - iconSize;
        const yLimit = height - iconSize;

        ctx.clearRect(0, 0, width, height);

        icons.sort((_a, _b) => _a.speed - _b.speed).forEach((left, i) => {
            var stillColliding = false;

            icons.sort((_a, _b) => _a.speed - _b.speed).slice(i).forEach(right => {
                const distanceX = Math.abs(left.posX - right.posX);
                const distanceY = Math.abs(left.posY - right.posY);

                const distance = Math.sqrt(Math.pow(distanceX, 2) + Math.pow(distanceY, 2));

                const absoluteDistanceX = distanceX * xLimit;
                const absoluteDistanceY = distanceY * yLimit;

                if (distance <= lineThreshold) {
                    ctx.beginPath();
                    
                    ctx.strokeStyle = lineColor;
                    ctx.moveTo(left.posX * xLimit + iconSize / 2, left.posY * yLimit + iconSize / 2);
                    ctx.lineTo(right.posX * xLimit + iconSize / 2, right.posY * yLimit + iconSize / 2);

                    ctx.stroke();
                }

                if (absoluteDistanceX <= iconSize && absoluteDistanceY <= iconSize) {
                    if (left.speed > right.speed) {
                        if (distanceX > distanceY) {
                            left.incX = !left.incX;
                            right.incX = !left.incX;
                        }
                        if (distanceY > distanceX) {
                            left.incY = !left.incY;
                            right.incY = !left.incY;
                        }
                        if (distanceX == distanceY) {
                            left.incX = !left.incX;
                            right.incX = !left.incX;
                            left.incY = !left.incY;
                            right.incY = !left.incY;
                        }
                    }
                    else {
                        if (distanceX > distanceY) {
                            right.incX = !right.incX;
                            left.incX = !right.incX;
                        }
                        if (distanceY > distanceX) {
                            right.incY = !right.incY;
                            left.incY = !right.incY;
                        }
                        if (distanceX == distanceY) {
                            right.incX = !right.incX;
                            left.incX = !right.incX;
                            right.incY = !right.incY;
                            left.incY = !right.incY;
                        }
                    }
                }
            });
        });

        icons.forEach(icon => {
            if (icon.posX >= 1 || icon.posX <= 0) {
                icon.incX = !icon.incX;
            }
            if (icon.posY >= 1 || icon.posY <= 0) {
                icon.incY = !icon.incY;
            }

            icon.posX = Math.max(0, Math.min(1, icon.posX + (icon.incX ? icon.speed : -icon.speed)));
            icon.posY = Math.max(0, Math.min(1, icon.posY + (icon.incY ? icon.speed : -icon.speed)));

            const absoluteX = icon.posX * xLimit;
            const absoluteY = icon.posY * yLimit;

            ctx.drawImage(icon.image, absoluteX, absoluteY, iconSize, iconSize);
        });

        window.requestAnimationFrame(draw);
    }

    window.requestAnimationFrame(draw);     
    
    interface IconAnimationState {
        image: HTMLImageElement;
        
        posX: number;
        posY: number;

        incX: boolean;
        incY: boolean;

        speed: number;
    }
});
</script>

<div class="w-full h-big" bind:this={container}>
    <canvas
        bind:this={canvas}
    >
    </canvas>
</div>


<style>
    .h-big {
        height: 32em;
    }
</style>