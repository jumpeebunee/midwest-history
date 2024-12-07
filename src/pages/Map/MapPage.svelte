<script lang="ts">
	let isDragging = $state(false);
	let startX = $state(0);
	let startY = $state(0);
	let initialLeft = $state(0);
	let initialTop = $state(0);
	let left = $state(0);
	let top = $state(0);

	const onMouseDown = (e: MouseEvent) => {
		isDragging = true;
		startX = e.clientX;
		startY = e.clientY;
		initialLeft = left;
		initialTop = top;
	};

	const onMouseMove = (e: MouseEvent) => {
		if (!isDragging) return;

		const dx = e.clientX - startX;
		const dy = e.clientY - startY;

		left = initialLeft + dx;
		top = initialTop + dy;
	};

	const onMouseUp = () => {
		isDragging = false;
	};
</script>

<div
	tabindex="0"
	role="button"
	onmouseup={onMouseUp}
	onmouseleave={onMouseUp}
	onmousedown={onMouseDown}
	onmousemove={onMouseMove}
	class="container {isDragging ? 'grabbing' : ''}"
>
	<div class="content" style="transform: translate({left}px, {top}px);">4</div>
</div>

<style>
	:global(body) {
		margin: 0;
		overflow: hidden;
	}

	.container {
		width: 100vw;
		height: 100vh;
		overflow: hidden;
		position: relative;
		cursor: grab;
		background: #fff0dd;
	}

	.container.grabbing {
		cursor: grabbing;
	}

	.content {
		left: 50%;
		top: 50%;
		position: absolute;
	}
</style>
