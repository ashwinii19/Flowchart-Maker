<script>
	import html2canvas from "html2canvas";

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
	let selectedShape = null;

	function addRectangle() {
		rectangles = [...rectangles, { id: rectangles.length, el: null, text: 'Rectangle', borderColor: selectedShapeColor1, backgroundColor: selectedShapeColor2, textColor: selectedTextColor }];
	}

	function addCircle() {
		circles = [...circles, { id: circles.length, el: null, text: 'Circle', borderColor: selectedShapeColor1, backgroundColor: selectedShapeColor2, textColor: selectedTextColor }];
	}

	function addOval() {
		ovals = [...ovals, { id: ovals.length, el: null, text: 'Oval', borderColor: selectedShapeColor1, backgroundColor: selectedShapeColor2, textColor: selectedTextColor }];
	}

	function addRhombus() {
		rhombuses = [...rhombuses, { id: rhombuses.length, el: null, text: 'Rhombus', borderColor: selectedShapeColor1, backgroundColor: selectedShapeColor2, textColor: selectedTextColor }];
	}

	function addParallelogram() {
		parallelograms = [...parallelograms, { id: parallelograms.length, el: null, text: 'Parallelogram', borderColor: selectedShapeColor1, backgroundColor: selectedShapeColor2, textColor: selectedTextColor }];
	}

	function addTriangle() {
		triangles = [...triangles, { id: triangles.length, el: null, text: 'Triangle', borderColor: selectedShapeColor1, backgroundColor: selectedShapeColor2, textColor: selectedTextColor }];
	}

	function addHexagon() {
		hexagons = [...hexagons, { id: hexagons.length, el: null, text: 'Hexagon', borderColor: selectedShapeColor1, backgroundColor: selectedShapeColor2, textColor: selectedTextColor }];
	}

	function addOr() {
		ors = [...ors, { id: ors.length, el: null, text: 'Or', borderColor: selectedShapeColor1, backgroundColor: selectedShapeColor2, textColor: selectedTextColor }];
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

	function selectShape(shape) {
		selectedShape = shape;
	}

	function applySelectedColor() {
		if (selectedShape) {
			selectedShape.borderColor = selectedShapeColor1;
			selectedShape.backgroundColor = selectedShapeColor2;
			selectedShape.textColor = selectedTextColor;
		}
	}

	function downloadAsImage() {
		const content = document.getElementById('content-to-download');
		html2canvas(content).then(canvas => {
			const link = document.createElement('a');
			link.href = canvas.toDataURL();
			link.download = 'flowchart.png';
			link.click();
		});
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
					<button on:click={applySelectedColor}>Apply Selected Color</button>
				</div>
				
				<button on:click={downloadAsImage}>Download as Image</button>
			</div>

			<div class="content" id="content-to-download">
				{#each rectangles as rect, index}
					<div bind:this={rect.el} class="rectangle" on:mousedown={handleMouseDown(index, 'move', 'rectangle')} style="border-color: {rect.borderColor}; background-color: {rect.backgroundColor};">
						<p contenteditable="true" style="color: {rect.textColor};">{rect.text}</p>
						<span class="resize-handle" on:mousedown={handleMouseDown(index, 'resize', 'rectangle')}></span>
						<button class="delete-btn" on:click={() => deleteShape(index, 'rectangle')}>X</button>
						<button class="select-btn" on:click={() => selectShape(rect)}>Select</button>
					</div>
				{/each}

				{#each circles as circ, index}
					<div bind:this={circ.el} class="circle" on:mousedown={handleMouseDown(index, 'move', 'circle')} style="border-color: {circ.borderColor}; background-color: {circ.backgroundColor};">
						<p contenteditable="true" style="color: {circ.textColor};">{circ.text}</p>
						<span class="resize-handle" on:mousedown={handleMouseDown(index, 'resize', 'circle')}></span>
						<button class="delete-btn" on:click={() => deleteShape(index, 'circle')}>X</button>
						<button class="select-btn" on:click={() => selectShape(circ)}>Select</button>
					</div>
				{/each}

				{#each ovals as ov, index}
					<div bind:this={ov.el} class="oval" on:mousedown={handleMouseDown(index, 'move', 'oval')} style="border-color: {ov.borderColor}; background-color: {ov.backgroundColor};">
						<p contenteditable="true" style="color: {ov.textColor};">{ov.text}</p>
						<span class="resize-handle" on:mousedown={handleMouseDown(index, 'resize', 'oval')}></span>
						<button class="delete-btn" on:click={() => deleteShape(index, 'oval')}>X</button>
						<button class="select-btn" on:click={() => selectShape(ov)}>Select</button>
					</div>
				{/each}

				{#each rhombuses as rho, index}
					<div bind:this={rho.el} class="rhombus" on:mousedown={handleMouseDown(index, 'move', 'rhombus')} style="border-color: {rho.borderColor}; background-color: {rho.backgroundColor};">
						<p contenteditable="true" style="color: {rho.textColor};">{rho.text}</p>
						<span class="resize-handle" on:mousedown={handleMouseDown(index, 'resize', 'rhombus')}></span>
						<button class="delete-btn" on:click={() => deleteShape(index, 'rhombus')}>X</button>
						<button class="select-btn" on:click={() => selectShape(rho)}>Select</button>
					</div>
				{/each}

				{#each parallelograms as para, index}
					<div bind:this={para.el} class="parallelogram" on:mousedown={handleMouseDown(index, 'move', 'parallelogram')} style="border-color: {para.borderColor}; background-color: {para.backgroundColor};">
						<p contenteditable="true" style="color: {para.textColor};">{para.text}</p>
						<span class="resize-handle" on:mousedown={handleMouseDown(index, 'resize', 'parallelogram')}></span>
						<button class="delete-btn" on:click={() => deleteShape(index, 'parallelogram')}>X</button>
						<button class="select-btn" on:click={() => selectShape(para)}>Select</button>
					</div>
				{/each}

				{#each triangles as tri, index}
					<div bind:this={tri.el} class="triangle" on:mousedown={handleMouseDown(index, 'move', 'triangle')} style="border-color: {tri.borderColor}; background-color: {tri.backgroundColor};">
						<p contenteditable="true" style="color: {tri.textColor};">{tri.text}</p>
						<span class="resize-handle" on:mousedown={handleMouseDown(index, 'resize', 'triangle')}></span>
						<button class="delete-btn" on:click={() => deleteShape(index, 'triangle')}>X</button>
						<button class="select-btn" on:click={() => selectShape(tri)}>Select</button>
					</div>
				{/each}

				{#each hexagons as hex, index}
					<div bind:this={hex.el} class="hexagon" on:mousedown={handleMouseDown(index, 'move', 'hexagon')} style="border-color: {hex.borderColor}; background-color: {hex.backgroundColor};">
						<p contenteditable="true" style="color: {hex.textColor};">{hex.text}</p>
						<span class="resize-handle" on:mousedown={handleMouseDown(index, 'resize', 'hexagon')}></span>
						<button class="delete-btn" on:click={() => deleteShape(index, 'hexagon')}>X</button>
						<button class="select-btn" on:click={() => selectShape(hex)}>Select</button>
					</div>
				{/each}

				{#each ors as orShape, index}
					<div bind:this={orShape.el} class="or-shape" on:mousedown={handleMouseDown(index, 'move', 'or')} style="border-color: {orShape.borderColor}; background-color: {orShape.backgroundColor};">
						<p contenteditable="true" style="color: {orShape.textColor};">{orShape.text}</p>
						<span class="resize-handle" on:mousedown={handleMouseDown(index, 'resize', 'or')}></span>
						<button class="delete-btn" on:click={() => deleteShape(index, 'or')}>X</button>
						<button class="select-btn" on:click={() => selectShape(orShape)}>Select</button>
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

	.delete-btn,
	.select-btn {
		position: absolute;
		top: 0;
		right: 0;
		background-color: red;
		color: white;
		border: none;
		cursor: pointer;
	}

	.select-btn {
		top: 25px;
		background-color: green;
	}

	p {
		margin: 0;
		text-align: center;
	}
</style>
