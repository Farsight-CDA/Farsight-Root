<script lang="ts">
	import bitcoin_logo from "$lib/images/currencies/bitcoin.svg";
	import ethereum_logo from "$lib/images/currencies/ethereum.svg";
	import polkadot_logo from "$lib/images/currencies/polkadot.svg";
	import cosmos_logo from "$lib/images/currencies/cosmos.svg";
	import avalanche_logo from "$lib/images/currencies/avalanche.svg";
	import flow_logo from "$lib/images/currencies/flow.svg";
	import solana_logo from "$lib/images/currencies/solana.svg";

	import {onMount} from "svelte";

	export let lineThreshold: number = 0.45;
	export let lineColor: string = "#f88a13";

	let canvas: HTMLCanvasElement;
	let container: HTMLDivElement;

	onMount(() => {
		const ctx = canvas.getContext("2d")!;

		const icons: IconAnimationState[] = [];

		let time = new Date().getTime();

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
			velX: 1.3 * Math.random() / 1000,
			velY: 1.3 * Math.random() / 1000,
			radius: 0.05,
			mass: 0.01,
		});
		icons.push({
			image: ethereum,
			posX: Math.random(),
			posY: Math.random(),
			velX: 1.3 * Math.random() / 1000,
			velY: 1.3 * Math.random() / 1000,
			radius: 0.05,
			mass: 0.01,
		});
		icons.push({
			image: polkadot,
			posX: Math.random(),
			posY: Math.random(),
			velX: 1.3 * Math.random() / 1000,
			velY: 1.3 * Math.random() / 1000,
			radius: 0.05,
			mass: 0.01,
		});
		icons.push({
			image: cosmos,
			posX: Math.random(),
			posY: Math.random(),
			velX: 1.3 * Math.random() / 1000,
			velY: 1.3 * Math.random() / 1000,
			radius: 0.05,
			mass: 0.01,
		});
		icons.push({
			image: avalanche,
			posX: Math.random(),
			posY: Math.random(),
			velX: 1.3 * Math.random() / 1000,
			velY: 1.3 * Math.random() / 1000,
			radius: 0.05,
			mass: 0.01,
		});
		icons.push({
			image: flow,
			posX: Math.random(),
			posY: Math.random(),
			velX: 1.3 * Math.random() / 1000,
			velY: 1.3 * Math.random() / 1000,
			radius: 0.05,
			mass: 0.01,
		});
		icons.push({
			image: solana,
			posX: Math.random(),
			posY: Math.random(),
			velX: 1.3 * Math.random() / 1000,
			velY: 1.3 * Math.random() / 1000,
			radius: 0.05,
			mass: 0.01,
		});


		function closestpointonline(x0: number, y0: number, lx1: number, ly1: number, lx2: number, ly2): [number, number] {
			let A1 = ly2 - ly1;
			let B1 = lx1 - lx2;
			let C1 = (ly2 - ly1) * lx1 + (lx1 - lx2) * ly1;
			let C2 = -B1 * x0 + A1 * y0;
			let det = A1 * A1 - -B1 * B1;
			let cx = 0;
			let cy = 0;
			if (det != 0) {
				cx = ((A1 * C1 - B1 * C2) / det);
				cy = ((A1 * C2 - -B1 * C1) / det);
			} else {
				cx = x0;
				cy = y0;
			}
			return [cx, cy];
		}

		function checkcirclecollide(a: IconAnimationState, b: IconAnimationState): boolean {

			return Math.abs((a.posX - b.posX) * (a.posX - b.posX) + (a.posY - b.posY) * (a.posY - b.posY)) < (a.radius - b.radius) * (a.radius - b.radius);
		}

		function checkcirclewallcollide(a: IconAnimationState): boolean {

			const x1 = a.posX;
			const y1 = a.posY;
			const r1 = a.radius;

			return x1 + r1 >= 1 || x1 - r1 <= 0 || y1 + r1 >= 1 || y1 - r1 <= 0;
		}

		function wallcolision(a: IconAnimationState) {
			if (a.posX + a.radius >= 1) {
				a.velX = -Math.abs(a.velX);
				a.posX = 1 - a.radius;
			}
			if (a.posX - a.radius <= 0) {
				a.velX = +Math.abs(a.velX);
				a.posX = a.radius;
			}

			if (a.posY + a.radius >= 1) {
				a.velY = -Math.abs(a.velY);
				a.posY = 1 - a.radius;
			}
			if (a.posY - a.radius <= 0) {
				a.velY = +Math.abs(a.velY);
				a.posY = a.radius;
			}
		}

		function circlecolision(circle1: IconAnimationState, circle2: IconAnimationState) {

			const d = closestpointonline(circle1.posX, circle1.posY,
				circle1.posX + circle1.velX, circle1.posY + circle1.velY, circle2.posX, circle2.posY);
			const closestdistsq = Math.pow(circle2.posX - d[0], 2) + Math.pow(circle2.posY - d[1], 2);

			const backdist = Math.sqrt(Math.pow(circle1.radius + circle2.radius, 2) - closestdistsq);
			const movementvectorlength = Math.sqrt(Math.pow(circle1.velX, 2) + Math.pow(circle1.velY, 2));
			const c_x = d[0] - backdist * (circle1.velX / movementvectorlength);
			const c_y = d[1] - backdist * (circle1.velY / movementvectorlength);

			const collisiondist = Math.sqrt(Math.pow(circle2.posX - c_x, 2) + Math.pow(circle2.posY - c_y, 2));
			const n_x = (circle2.posX - c_x) / collisiondist;
			const n_y = (circle2.posY - c_y) / collisiondist;
			const p = 2 * (circle1.velX * n_x + circle1.velY * n_y) /
				(circle1.mass + circle2.mass);
			const w_x = circle1.velX - p * circle1.mass * n_x - p * circle2.mass * n_x;
			const w_y = circle2.velY - p * circle1.mass * n_y - p * circle2.mass * n_y;

			const dd = Math.sqrt(Math.pow(circle1.posX - circle2.posX, 2) + Math.pow(circle1.posY - circle2.posY, 2));
			const nx = (circle2.posX - circle1.posX) / dd;
			const ny = (circle2.posY - circle1.posY) / dd;
			const pp = 2 * (circle1.velX * nx + circle1.velY * n_y - circle2.velX * nx - circle2.velY * n_y) /
				(circle1.mass + circle2.mass);
			const vx1 = circle1.velX - pp * circle1.mass * n_x;
			const vy1 = circle1.velY - pp * circle1.mass * n_y;
			const vx2 = circle2.velX + pp * circle2.mass * n_x;
			const vy2 = circle2.velY + pp * circle2.mass * n_y;

			circle1.velX = vx1;
			circle1.velY = vy1;
			circle2.velX = vx2;
			circle2.velY = vy2;
		}

		function update() {
			icons.forEach((icon) => {

				const timeNow = Date.now();

				const timeDelta = Math.abs(time - timeNow) * 0.1;

				time = timeNow;

				icon.posX = icon.posX + icon.velX * timeDelta;
				icon.posY = icon.posY + icon.velY * timeDelta;

				if (checkcirclewallcollide(icon)) {
					wallcolision(icon);
				}
				icons.forEach((otherIcon) => {
					if (icon == otherIcon) {
						return;
					}
					if (checkcirclecollide(icon, otherIcon)) {
						circlecolision(icon, otherIcon);
					}
				})

				console.log(icon)

			});
		}


		function render() {
			update();
			const width = container.clientWidth;
			const height = container.clientHeight;

			canvas.width = width;
			canvas.height = height;


			ctx.clearRect(0, 0, width, height);

			icons.sort((_a, _b) => _a.posX - _b.posX).forEach((left, i) => {

				icons.sort((_a, _b) => _a.posX - _b.posX).slice(i).forEach(right => {
					const distanceX = Math.abs(left.posX - right.posX);
					const distanceY = Math.abs(left.posY - right.posY);

					const distance = Math.sqrt(Math.pow(distanceX, 2) + Math.pow(distanceY, 2));

					const middlePointLeftX = left.posX + left.radius;
					const middlePointLeftY = left.posX + left.radius;
					const middlePointRightX = right.posX + right.radius;
					const middlePointRightY = right.posX + right.radius;

					if (distance <= lineThreshold) {
						ctx.beginPath();

						ctx.strokeStyle = lineColor;
						ctx.moveTo(middlePointLeftX * width,middlePointLeftY * height);
						ctx.lineTo(middlePointRightX * width,middlePointLeftY * height);

						ctx.stroke();
					}
				});
			});


			icons.forEach(icon => {

				const absoluteX = icon.posX * width;
				const absoluteY = icon.posY * height;
				const iconSizeX = icon.radius * width;
				const iconSizeY = icon.radius * height;

				ctx.drawImage(icon.image, absoluteX, absoluteY, iconSizeX, iconSizeY);
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