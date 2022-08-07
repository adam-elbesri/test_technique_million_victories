<script>
	export let value;
	export let min;
	export let max;
	export let precision;
	$: step = 1 / Math.pow(10, precision);

	const handleChange = (e) => {
		value = e.target.value;

		if (value > max && typeof max !== 'undefined') {
			value = max;
		} else if (value < min && typeof min !== 'undefined') {
			value = min;
		}

		if (precision !== 'undefined') {
			value = Math.trunc(value * Math.pow(10, precision)) / Math.pow(10, precision);
		}
	};
</script>

<div
	class="tooltip tooltip-right"
	data-tip="Max: {max ?? 'none'} |  Min: {min ?? 'none'} | Precision: {precision ?? 'none'}"
>
	<input
		type="number"
		{step}
		min={min ?? ''}
		max={max ?? ''}
		bind:value
		class="input input-bordered w-full border-accent"
		on:change={handleChange}
	/>
</div>
