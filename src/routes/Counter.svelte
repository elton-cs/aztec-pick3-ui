<script lang="ts">
	import { spring } from 'svelte/motion';

	let count = 0;
	let disablePlus = false;
	let disableMinus = false;

	function increase() {
		if (count > 8) {
			count = 0
		} else {
			count += 1
		}
	}

	function decrease() {
		if (count < 1) {
			count = 9
		} else {
			count -= 1
		}
	}

	const displayed_count = spring();
	$: displayed_count.set(count);
	$: offset = modulo($displayed_count, 1);

	function modulo(n: number, m: number) {
		// handle negative numbers
		return ((n % m) + m) % m;
		// return (n + 10);
	}
</script>

<div class="counter flex flex-col items-center space-y-3">

    <button class="bg-white hover:bg-gray-100 text-gray-800 font-semibold py-2 px-4 border border-gray-400 rounded shadow" 
	on:click={() => increase() } aria-label="Increase the counter by one">
		+
	</button>

	<div class="counter-viewport">
		<div class="counter-digits" style="transform: translate(0, {100 * offset}%)">
			<strong class="hidden" aria-hidden="true">{Math.floor($displayed_count + 1)}</strong>
			<strong >{Math.floor($displayed_count)}</strong>
		</div>
	</div>

    <button class="bg-white hover:bg-gray-100 text-gray-800 font-semibold py-2 px-4 border border-gray-400 rounded shadow"
	on:click={() => decrease()} aria-label="Decrease the counter by one">
		-
	</button>
    
</div>

<style>
	.counter {
		display: flex;
		/* border-top: 1px solid rgba(0, 0, 0, 0.1); */
		/* border-bottom: 1px solid rgba(0, 0, 0, 0.1); */
		margin: 1rem 0;
	}

	/* .counter button {
		width: 2em;
		padding: 0;
		display: flex;
		align-items: center;
		justify-content: center;
		border: 0;
		background-color: transparent;
		touch-action: manipulation;
		font-size: 2rem;
	} */

	/* .counter button:hover {
		background-color: var(--color-bg-1);
	} */

	svg {
		width: 25%;
		height: 25%;
	}

	path {
		vector-effect: non-scaling-stroke;
		stroke-width: 2px;
		stroke: #444;
	}

	.counter-viewport {
		width: 8em;
		height: 4em;
		overflow: hidden;
		text-align: center;
		position: relative;
	}

	.counter-viewport strong {
		position: absolute;
		display: flex;
		width: 100%;
		height: 100%;
		font-weight: 400;
		/* color: var(--color-theme-1); */
		font-size: 4rem;
		align-items: center;
		justify-content: center;
	}

	.counter-digits {
		position: absolute;
		width: 100%;
		height: 100%;
	}

	.hidden {
		top: -100%;
		user-select: none;
	}
</style>
