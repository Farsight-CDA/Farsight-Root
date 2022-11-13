<script lang="ts">
	import bitcoin_logo from "$lib/images/currencies/bitcoin.svg";
	import ethereum_logo from "$lib/images/currencies/ethereum.svg";
	import polkadot_logo from "$lib/images/currencies/polkadot.svg";
	import cosmos_logo from "$lib/images/currencies/cosmos.svg";
	import avalanche_logo from "$lib/images/currencies/avalanche.svg";
	import flow_logo from "$lib/images/currencies/flow.svg";
	import binance_logo from "$lib/images/currencies/binance.svg";
	import doge_logo from "$lib/images/currencies/doge.svg"

	import {onMount} from "svelte";

	export let lineThreshold: number = 0.45;
	export let lineColor: string = "#f88a13";
	export let speed: number = 0.06;
	export let iconSize: number = 0.75;

	let canvas: HTMLCanvasElement;
	let container: HTMLDivElement;

	let xWall: number = 1;
	let yWall: number = 1;

	let mouseX: number = -1;
	let mouseY: number = -1;

	function handleMouseMove(o: MouseEvent) {
		mouseX = o.offsetX;
		mouseY = o.offsetY;
	}
	function handleMouseLeave() {
		mouseX = -1;
		mouseY = -1;
	}

	onMount(() => {
		function makeIcon(image: string): IconAnimationState {
			var img = new Image();
			img.src = image;
			return {
				image: img,
				posX: Math.random(),
				posY: Math.random(),
				velX: 1.3 * Math.random() / 1000,
				velY: 1.3 * Math.random() / 1000,
				radius: iconSize * (Math.random() / 2 + 0.25) / 10,
				mass: 0.1,
				hover: false
			}
		}	

		const ctx = canvas.getContext("2d")!;

		let time = new Date().getTime();

		const icons = [
			makeIcon(bitcoin_logo),
			makeIcon(ethereum_logo),
			makeIcon(polkadot_logo),
			makeIcon(cosmos_logo),
			makeIcon(avalanche_logo),
			makeIcon(flow_logo),
			makeIcon(binance_logo),
			makeIcon(doge_logo)
		];

		function checkcirclecollide(a: IconAnimationState, b: IconAnimationState): boolean {
			const isColliding = Math.abs((a.posX - b.posX) * (a.posX - b.posX) + (a.posY - b.posY) * (a.posY - b.posY)) < (a.radius + b.radius) * (a.radius + b.radius);
			return isColliding;
		}

		function checkcirclewallcollide(circle: IconAnimationState): boolean {
			const isColliding = circle.posX + circle.radius >= xWall || 
								circle.posX - circle.radius <= 0 || 
								circle.posY + circle.radius >= yWall || 
								circle.posY - circle.radius <= 0;

			return isColliding;
		}

		function wallcolision(a: IconAnimationState) {
			if (a.posX + a.radius >= xWall) {
				a.velX = 0 - Math.abs(a.velX);
				a.posX = xWall - a.radius;
			}
			if (a.posX - a.radius <= 0) {
				a.velX = +Math.abs(a.velX);
				a.posX = a.radius;
			}

			if (a.posY + a.radius >= yWall) {
				a.velY = -Math.abs(a.velY);
				a.posY = yWall - a.radius;
			}
			if (a.posY - a.radius <= 0) {
				a.velY = +Math.abs(a.velY);
				a.posY = a.radius;
			}
		}

		function circlecolision(circle1: IconAnimationState, circle2: IconAnimationState) {
			const distanceBetweenCircles = Math.sqrt(Math.pow(circle1.posX - circle2.posX, 2) + Math.pow(circle1.posY - circle2.posY, 2));
			const distanceToMove = circle1.radius + circle2.radius - distanceBetweenCircles;
			const angle = Math.atan2(circle2.posY - circle1.posY, circle2.posX - circle1.posX);

			const nx = (circle2.posX - circle1.posX) / distanceBetweenCircles;
			const ny = (circle2.posY - circle1.posY) / distanceBetweenCircles;

			const pp = 2 * (circle1.velX * nx + circle1.velY * ny - circle2.velX * nx - circle2.velY * ny) /
				(circle1.mass + circle2.mass);

			circle2.posX += (Math.cos(angle) * distanceToMove);
			circle2.posY += (Math.sin(angle) * distanceToMove);

			circle1.velX = circle1.velX - pp * circle1.mass * nx;
			circle1.velY = circle1.velY - pp * circle1.mass * ny;
			circle2.velX = circle2.velX + pp * circle2.mass * nx;
			circle2.velY = circle2.velY + pp * circle2.mass * ny;
		}

		function update() {
			const timeNow = Date.now();
			const timeDelta = Math.abs(time - timeNow) * speed;
			time = timeNow;

			icons.sort(x => x.radius).forEach((icon) => {
				icon.posX = icon.posX + icon.velX * timeDelta;
				icon.posY = icon.posY + icon.velY * timeDelta;

				icons.forEach((otherIcon) => {
					if (icon == otherIcon) {
						return;
					}

					if (checkcirclecollide(icon, otherIcon)) {
						circlecolision(icon, otherIcon);
					}
				});

				if (checkcirclewallcollide(icon)) {
					wallcolision(icon);
				}
			});
		}


		function render() {
			update();
			const width = container.clientWidth;
			const height = container.clientHeight;
			const widthToHeightRatio = width / height;

			yWall = height / width;

			canvas.width = width;
			canvas.height = height;

			ctx.clearRect(0, 0, width, height);

			icons.forEach(icon => {
				const absoluteRadiusX = icon.radius * width;
				const absoluteRadiusY = widthToHeightRatio * icon.radius * height;

				const absoluteMiddleX = icon.posX * width;
				const absoluteMiddleY = widthToHeightRatio * icon.posY * height;

				if (Math.abs(absoluteMiddleX - mouseX) < absoluteRadiusX && Math.abs(absoluteMiddleY - mouseY) < absoluteRadiusY) {
					icon.hover = true;
				}
				else {
					icon.hover = false;
				}
			});

			icons.sort((_a, _b) => _a.posX - _b.posX).forEach((left, i) => {

				icons.sort((_a, _b) => _a.posX - _b.posX).slice(i).forEach(right => {
					const distanceX = Math.abs(left.posX - right.posX);
					const distanceY = Math.abs(left.posY - right.posY);

					const distance = Math.sqrt(Math.pow(distanceX, 2) + Math.pow(distanceY, 2));

					if (distance <= lineThreshold) {
						ctx.beginPath();

						if (left.hover || right.hover) {
							ctx.strokeStyle = "#ffffff";
							ctx.lineWidth = 6;
						}
						else {
							ctx.strokeStyle = lineColor;
							ctx.lineWidth = 1;
						}

						ctx.moveTo(left.posX * width, left.posY * height * widthToHeightRatio);
						ctx.lineTo(right.posX * width, right.posY * height * widthToHeightRatio);

						ctx.stroke();
					}
				});
			});

			icons.forEach(icon => {
				const absoluteRadiusX = icon.radius * width;
				const absoluteRadiusY = widthToHeightRatio * icon.radius * height;

				const absoluteMiddleX = icon.posX * width;
				const absoluteMiddleY = widthToHeightRatio * icon.posY * height;

				const absoluteX = absoluteMiddleX - absoluteRadiusX;
				const absoluteY = absoluteMiddleY - absoluteRadiusY;

				if (Math.abs(absoluteMiddleX - mouseX) < absoluteRadiusX && Math.abs(absoluteMiddleY - mouseY) < absoluteRadiusY) {
					icon.hover = true;
				}
				else {
					icon.hover = false;
				}

				ctx.drawImage(icon.image, absoluteX, absoluteY, 2 * icon.radius * width, 2 * icon.radius * height * widthToHeightRatio);
			});

			window.requestAnimationFrame(render);
		}

		window.requestAnimationFrame(render);

		interface IconAnimationState {
			image: HTMLImageElement;

			posX: number;
			posY: number;

			velX: number;
			velY: number;

			mass: number;
			radius: number;

			hover: boolean;
		}
	});
</script>

<div class="w-full h-big" bind:this={container}>
    <canvas
		bind:this={canvas}
		on:mousemove={handleMouseMove}
		on:mouseleave={handleMouseLeave}
    >
    </canvas>
</div>


<style>
    .h-big {
        height: 32em;
    }
</style>