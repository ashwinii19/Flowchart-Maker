<script>
	import { onMount } from "svelte";

	let rectangles = [];
	let circles = [];
	let ovals = [];
	let rhombuses = [];
	let parallelograms = [];
	let triangles = [];
	let hexagons = [];
	let ors = [];
	let isLoggedIn = true;

	let selectedShapeColor1 = "#000000";
	let selectedShapeColor2 = "#ffffff";
	let selectedTextColor = "#000000";

	function addRectangle() {
		rectangles = [...rectangles, { id: rectangles.length, el: null, text: "Rectangle" }];
	}

	function addCircle() {
		circles = [...circles, { id: circles.length, el: null, text: "Circle" }];
	}

	function addOval() {
		ovals = [...ovals, { id: ovals.length, el: null, text: "Oval" }];
	}

	function addRhombus() {
		rhombuses = [...rhombuses, { id: rhombuses.length, el: null, text: "Rhombus" }];
	}

	function addParallelogram() {
		parallelograms = [...parallelograms, { id: parallelograms.length, el: null, text: "Parallelogram" }];
	}

	function addTriangle() {
		triangles = [...triangles, { id: triangles.length, el: null, text: "Triangle" }];
	}

	function addHexagon() {
		hexagons = [...hexagons, { id: hexagons.length, el: null, text: "Hexagon" }];
	}

	function addOr() {
		ors = [...ors, { id: ors.length, el: null, text: "Or" }];
	}

	function handleMouseDown(index, action, type) {
		return function (event) {
			event.preventDefault();

			let element;
			switch (type) {
				case 'rectangle':
					element = rectangles[index].el;
					break;
				case 'circle':
					element = circles[index].el;
					break;
				case 'oval':
					element = ovals[index].el;
					break;
				case 'rhombus':
					element = rhombuses[index].el;
					break;
				case 'parallelogram':
					element = parallelograms[index].el;
					break;
				case 'triangle':
					element = triangles[index].el;
					break;
				case 'hexagon':
					element = hexagons[index].el;
					break;
				case 'or':
					element = ors[index].el;
					break;
			}

			let startX = event.clientX;
			let startY = event.clientY;
			let startWidth = element.offsetWidth;
			let startHeight = element.offsetHeight;
			let startLeft = element.offsetLeft;
			let startTop = element.offsetTop;

			function onMouseMove(event) {
				if (action === 'move') {
					const dx = event.clientX - startX;
					const dy = event.clientY - startY;
					element.style.left = `${startLeft + dx}px`;
					element.style.top = `${startTop + dy}px`;
				} else if (action === 'resize') {
					const dx = event.clientX - startX;
					const dy = event.clientY - startY;
					element.style.width = `${startWidth + dx}px`;
					element.style.height = `${startHeight + dy}px`;
				}
			}

			function onMouseUp() {
				document.removeEventListener('mousemove', onMouseMove);
				document.removeEventListener('mouseup', onMouseUp);
			}

			document.addEventListener('mousemove', onMouseMove);
			document.addEventListener('mouseup', onMouseUp);
		};
	}

	function deleteShape(index, type) {
		switch (type) {
			case 'rectangle':
				rectangles = rectangles.filter((_, i) => i !== index);
				break;
			case 'circle':
				circles = circles.filter((_, i) => i !== index);
				break;
			case 'oval':
				ovals = ovals.filter((_, i) => i !== index);
				break;
			case 'rhombus':
				rhombuses = rhombuses.filter((_, i) => i !== index);
				break;
			case 'parallelogram':
				parallelograms = parallelograms.filter((_, i) => i !== index);
				break;
			case 'triangle':
				triangles = triangles.filter((_, i) => i !== index);
				break;
			case 'hexagon':
				hexagons = hexagons.filter((_, i) => i !== index);
				break;
			case 'or':
				ors = ors.filter((_, i) => i !== index);
				break;
		}
	}

	function changeShapeColor(index, type) {
		let shape;
		switch (type) {
			case 'rectangle':
				shape = rectangles[index];
				break;
			case 'circle':
				shape = circles[index];
				break;
			case 'oval':
				shape = ovals[index];
				break;
			case 'rhombus':
				shape = rhombuses[index];
				break;
			case 'parallelogram':
				shape = parallelograms[index];
				break;
			case 'triangle':
				shape = triangles[index];
				break;
			case 'hexagon':
				shape = hexagons[index];
				break;
			case 'or':
				shape = ors[index];
				break;
		}
		if (shape.el) {
			shape.el.style.borderColor = selectedShapeColor1;
			shape.el.style.backgroundColor = selectedShapeColor2;
		}
	}

	function changeTextColor(index, type) {
		let shape;
		switch (type) {
			case 'rectangle':
				shape = rectangles[index];
				break;
			case 'circle':
				shape = circles[index];
				break;
			case 'oval':
				shape = ovals[index];
				break;
			case 'rhombus':
				shape = rhombuses[index];
				break;
			case 'parallelogram':
				shape = parallelograms[index];
				break;
			case 'triangle':
				shape = triangles[index];
				break;
			case 'hexagon':
				shape = hexagons[index];
				break;
			case 'or':
				shape = ors[index];
				break;
		}
		if (shape.el) {
			const text = shape.el.querySelector('p');
			if (text) {
				text.style.color = selectedTextColor;
			}
		}
	}
</script>

<div class="dashboardbody">
	{#if isLoggedIn}
		<div class="main-content">
			<div class="sidebar">
				<div class="elements-section">
					<h2>Flowchart Elements:</h2>
					<button on:click={addRectangle}>Add Rectangle</button>
					<button on:click={addCircle}>Add Circle</button>
					<button on:click={addOval}>Add Oval</button>
					<button on:click={addRhombus}>Add Rhombus</button>
					<button on:click={addParallelogram}>Add Parallelogram</button>
					<button on:click={addTriangle}>Add Triangle</button>
					<button on:click={addHexagon}>Add Hexagon</button>
					<button on:click={addOr}>Add Or</button>
				</div>

				<div class="color-section">
					<label for="shapeBorderColor">Shape Border Color:</label>
					<input type="color" id="shapeBorderColor" bind:value={selectedShapeColor1}>
				
					<label for="shapeBackgroundColor">Shape Background Color:</label>
					<input type="color" id="shapeBackgroundColor" bind:value={selectedShapeColor2}>
				
					<label for="textColor">Text Color:</label>
					<input type="color" id="textColor" bind:value={selectedTextColor}>
				</div>
				
			</div>

			<div class="content" id="content-to-download">
				{#each rectangles as rect, index}
					<div bind:this={rect.el} class="rectangle" on:mousedown={handleMouseDown(index, 'move', 'rectangle')}>
						<input type="text" bind:value={rect.text} />
						<p>{rect.text}</p>
						<span class="resize-handle" on:mousedown={handleMouseDown(index, 'resize', 'rectangle')}></span>
						<button class="delete-btn" on:click={() => deleteShape(index, 'rectangle')}>X</button>
						<button class="color-btn" on:click={() => changeShapeColor(index, 'rectangle')}>Color</button>
						<button class="text-btn" on:click={() => changeTextColor(index, 'rectangle')}>Text</button>
					</div>
				{/each}

				{#each circles as circ, index}
					<div bind:this={circ.el} class="circle" on:mousedown={handleMouseDown(index, 'move', 'circle')}>
						<input type="text" bind:value={circ.text} />
						<p>{circ.text}</p>
						<span class="resize-handle" on:mousedown={handleMouseDown(index, 'resize', 'circle')}></span>
						<button class="delete-btn" on:click={() => deleteShape(index, 'circle')}>X</button>
						<button class="color-btn" on:click={() => changeShapeColor(index, 'circle')}>Color</button>
						<button class="text-btn" on:click={() => changeTextColor(index, 'circle')}>Text</button>
					</div>
				{/each}

				{#each ovals as ov, index}
					<div bind:this={ov.el} class="oval" on:mousedown={handleMouseDown(index, 'move', 'oval')}>
						<input type="text" bind:value={ov.text} />
						<p>{ov.text}</p>
						<span class="resize-handle" on:mousedown={handleMouseDown(index, 'resize', 'oval')}></span>
						<button class="delete-btn" on:click={() => deleteShape(index, 'oval')}>X</button>
						<button class="color-btn" on:click={() => changeShapeColor(index, 'oval')}>Color</button>
						<button class="text-btn" on:click={() => changeTextColor(index, 'oval')}>Text</button>
					</div>
				{/each}

				{#each rhombuses as rho, index}
					<div bind:this={rho.el} class="rhombus" on:mousedown={handleMouseDown(index, 'move', 'rhombus')}>
						<input type="text" bind:value={rho.text} />
						<p>{rho.text}</p>
						<span class="resize-handle" on:mousedown={handleMouseDown(index, 'resize', 'rhombus')}></span>
						<button class="delete-btn" on:click={() => deleteShape(index, 'rhombus')}>X</button>
						<button class="color-btn" on:click={() => changeShapeColor(index, 'rhombus')}>Color</button>
						<button class="text-btn" on:click={() => changeTextColor(index, 'rhombus')}>Text</button>
					</div>
				{/each}

				{#each parallelograms as para, index}
					<div bind:this={para.el} class="parallelogram" on:mousedown={handleMouseDown(index, 'move', 'parallelogram')}>
						<input type="text" bind:value={para.text} />
						<p>{para.text}</p>
						<span class="resize-handle" on:mousedown={handleMouseDown(index, 'resize', 'parallelogram')}></span>
						<button class="delete-btn" on:click={() => deleteShape(index, 'parallelogram')}>X</button>
						<button class="color-btn" on:click={() => changeShapeColor(index, 'parallelogram')}>Color</button>
						<button class="text-btn" on:click={() => changeTextColor(index, 'parallelogram')}>Text</button>
					</div>
				{/each}

				{#each triangles as tri, index}
					<div bind:this={tri.el} class="triangle" on:mousedown={handleMouseDown(index, 'move', 'triangle')}>
						<input type="text" bind:value={tri.text} />
						<p>{tri.text}</p>
						<span class="resize-handle" on:mousedown={handleMouseDown(index, 'resize', 'triangle')}></span>
						<button class="delete-btn" on:click={() => deleteShape(index, 'triangle')}>X</button>
						<button class="color-btn" on:click={() => changeShapeColor(index, 'triangle')}>Color</button>
						<button class="text-btn" on:click={() => changeTextColor(index, 'triangle')}>Text</button>
					</div>
				{/each}

				{#each hexagons as hex, index}
					<div bind:this={hex.el} class="hexagon" on:mousedown={handleMouseDown(index, 'move', 'hexagon')}>
						<input type="text" bind:value={hex.text} />
						<p>{hex.text}</p>
						<span class="resize-handle" on:mousedown={handleMouseDown(index, 'resize', 'hexagon')}></span>
						<button class="delete-btn" on:click={() => deleteShape(index, 'hexagon')}>X</button>
						<button class="color-btn" on:click={() => changeShapeColor(index, 'hexagon')}>Color</button>
						<button class="text-btn" on:click={() => changeTextColor(index, 'hexagon')}>Text</button>
					</div>
				{/each}

				{#each ors as orShape, index}
					<div bind:this={orShape.el} class="or-shape" on:mousedown={handleMouseDown(index, 'move', 'or')}>
						<input type="text" bind:value={orShape.text} />
						<p>{orShape.text}</p>
						<span class="resize-handle" on:mousedown={handleMouseDown(index, 'resize', 'or')}></span>
						<button class="delete-btn" on:click={() => deleteShape(index, 'or')}>X</button>
						<button class="color-btn" on:click={() => changeShapeColor(index, 'or')}>Color</button>
						<button class="text-btn" on:click={() => changeTextColor(index, 'or')}>Text</button>
					</div>
				{/each}
			</div>
		</div>
	{/if}
</div>

<style>
	.dashboardbody {
		display: flex;
	}

	.main-content {
		display: flex;
		width: 100%;
	}

	.sidebar {
		width: 250px;
		background-color: #f0f0f0;
		padding: 20px;
		box-shadow: 2px 0 5px rgba(0, 0, 0, 0.1);
	}

	.elements-section,
	.color-section {
		margin-bottom: 20px;
	}

	.elements-section button {
		display: block;
		width: 100%;
		margin-bottom: 10px;
		padding: 10px;
		background-color: #007bff;
		color: white;
		border: none;
		cursor: pointer;
	}

	.elements-section button:hover {
		background-color: #0056b3;
	}

	.color-section label {
		display: block;
		margin-bottom: 5px;
	}

	.color-section input {
		display: block;
		width: 100%;
		margin-bottom: 10px;
	}

	.color-section button {
		display: block;
		width: 100%;
		padding: 10px;
		background-color: #28a745;
		color: white;
		border: none;
		cursor: pointer;
	}

	.color-section button:hover {
		background-color: #218838;
	}

	.content {
		flex-grow: 1;
		position: relative;
		background-color: #ffffff;
		border: 1px solid #dcdcdc;
		margin: 20px;
		padding: 10px;
	}

	.rectangle,
	.circle,
	.oval,
	.rhombus,
	.parallelogram,
	.triangle,
	.hexagon,
	.or-shape {
		position: absolute;
		padding: 20px;
		border: 2px solid #000;
		background-color: #fff;
		cursor: move;
		display: flex;
		justify-content: center;
		align-items: center;
	}

	.rectangle {
		width: 100px;
		height: 60px;
	}

	.circle {
		width: 100px;
		height: 100px;
		border-radius: 50%;
	}

	.oval {
		width: 150px;
		height: 100px;
		border-radius: 50%;
	}

	.rhombus {
		width: 100px;
		height: 100px;
		transform: rotate(45deg);
	}

	.parallelogram {
		width: 120px;
		height: 60px;
		transform: skew(20deg);
	}

	.triangle {
		width: 0;
		height: 0;
		border-left: 50px solid transparent;
		border-right: 50px solid transparent;
		border-bottom: 100px solid #000;
	}

	.hexagon {
		width: 100px;
		height: 55px;
		background-color: #fff;
		position: relative;
		margin: 55px 0;
	}

	.hexagon:before,
	.hexagon:after {
		content: "";
		position: absolute;
		width: 0;
		border-left: 50px solid transparent;
		border-right: 50px solid transparent;
	}

	.hexagon:before {
		bottom: 100%;
		border-bottom: 27.5px solid #000;
	}

	.hexagon:after {
		top: 100%;
		width: 0;
		border-top: 27.5px solid #000;
	}

	.or-shape {
		width: 80px;
		height: 80px;
		border-radius: 50%;
	}

	.resize-handle {
		position: absolute;
		right: 0;
		bottom: 0;
		width: 10px;
		height: 10px;
		background-color: #000;
		cursor: se-resize;
	}

	.delete-btn {
		position: absolute;
		top: 0;
		right: 0;
		background-color: red;
		color: white;
		border: none;
		cursor: pointer;
	}

	.color-btn,
	.text-btn {
		position: absolute;
		top: 0;
		left: 0;
		background-color: blue;
		color: white;
		border: none;
		cursor: pointer;
	}

	.color-btn {
		top: auto;
		bottom: 0;
	}

	.text-btn {
		left: auto;
		right: 0;
	}

	input[type="text"] {
		position: absolute;
		bottom: -20px;
		width: 100%;
		text-align: center;
		border: none;
	}
</style>
