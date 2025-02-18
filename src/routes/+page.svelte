<script lang="ts">
	import { elasticOut } from 'svelte/easing';

	let count = $state(0);
	let ypos = $state('60%');
	let xpos = $state('50%');

	function clickHandler(event: MouseEvent) {
		increment();
		const target = event.currentTarget as HTMLElement;
		randomPos(target);
	}

	function increment() {
		count += 1;
	}

	function getRandomInt(max: number) {
		return Math.floor(Math.random() * max);
	}

	function randomPos(target: HTMLElement) {
		const width = window.innerWidth - target.offsetWidth;
		const height = window.innerHeight - target.offsetHeight;
		xpos = `${getRandomInt(width)}px`;
		ypos = `${getRandomInt(height)}px`;
	}

	function spin(node: HTMLElement, { duration }: { duration: number }) {
		return {
			duration,
			// eslint-disable-next-line @typescript-eslint/no-unused-vars
			css: (t: number, _: unknown) => {
				const eased = elasticOut(t);

				return `
					transform: translate(-50%, -50%) scale(${eased}) rotate(${eased * 1080 + 2 * count}deg);
					`;
			}
		};
	}
</script>

<svelte:head><title>SvelteClick</title></svelte:head>

{#if count > 0 && count % 5 === 0}
	<h1 style="--count:{2 * count}deg" in:spin={{ duration: 2000 }}>
		<a href="https://github.com/dmoerner/svelteclick">Welcome to SvelteClick</a>
	</h1>
{:else}
	<h1 style="--count:{2 * count}deg">
		<a href="https://github.com/dmoerner/svelteclick">Welcome to SvelteClick</a>
	</h1>
{/if}

<button style="--ypos:{ypos}; --xpos:{xpos}" onclick={clickHandler}>
	{#if count === 0}
		Click me!
	{:else}
		{count}
	{/if}
</button>

<style>
	h1 {
		position: absolute;
		top: 50%;
		left: 50%;
		transform: translate(-50%, -50%) rotate(var(--count));
		transition: transform 1s;
		color: rebeccapurple;
	}

	a {
		text-decoration: none;
		color: rebeccapurple;
	}

	button {
		color: rebeccapurple;
		border: 0px;
		padding: 10px;
		border-radius: 8px;
		position: fixed;
		top: var(--ypos);
		left: var(--xpos);
		transform: translate(-50%);
		font-size: 20px;
	}
</style>
