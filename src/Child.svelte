<svelte:options accessors={true}/>
<script lang="ts">

	export let value;
	export let reset;
	export let selected = false;
	let isCtrlKey;

	const onInput = (event) => {
		const {relatedTarget, target} = event;
		if(relatedTarget?.classList.contains('ctrl-active')) {
			selected = true;
			isCtrlKey = false;
		} else {
			selected = false;
			isCtrlKey = false;
			reset();
		}
		value = parseFloat(target.value)
	}
	const onChange = e => {
		if(selected) {
			value =parseFloat(e.target.value)
		}
	}

	const onFocus = () => {
		selected = true;
	}
	const ctrlKey = ({ctrlKey}) => {
		if (ctrlKey) {
			isCtrlKey = true;
		} else {
			isCtrlKey = false;
		}
	}
</script>

<input class:selected class:ctrl-active={isCtrlKey} class="item" type="number" value={value} on:change={onChange} on:blur={onInput} on:focus={onFocus} on:mousedown={ctrlKey} on:mouseup={ctrlKey}>


<style>
	.item {
		box-sizing: border-box;
		width:  100%;
		border: 1px solid;
	}
	.item:focus-visible {
		/* border: none; */
		outline:  none;
	}
	.item.selected {
		border: 1px solid red;
		background-color: rgba(255, 0, 0, .1)
		
	}

	.item.ctrl-active {
		border: 3px solid red;
		background-color: rgba(255, 0, 0, .1)
	}

</style>