<script>
    import { onMount } from 'svelte';

    let currentPage = 'home';

    function navigate(page) {
        currentPage = page;
    }

    onMount(() => {
        console.log('Component mounted');
    });
</script>


<div class="card gap-16 items-center mx-auto max-w-screen-xl overflow-hidden rounded-lg">
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.0.0-beta3/css/all.min.css" integrity="sha512-Fo3rlrZj/k7ujTnHg4CGR2D7kSs0v4LLanw2qksYuRlEzO+tcaEPQogQ0KaoGN26/zrn20ImR1DfuLWnOo7aBA==" crossorigin="anonymous" referrerpolicy="no-referrer" />

    {#if currentPage === 'home'}
        <div class="mainbody">
            <div class="top">
                <div class="search"></div>
            </div>
        
            <div class="heading">
                <div class="left">
                    <p><marquee>Streamline Your Workflow with Clarity</marquee></p>
                    <p>The ultimate tool for transforming complex ideas into <br>clear visual representation. Streamline your workflow <br> with user-friendly, drag and drop flowchart creations<br>& effortlessly design professional diagrams in minute</p>
                    <p>Let's start to make your own flowchart</p>
                    <button on:click={() => navigate('about')}>Let's Make </button>
                </div>
        
                <div class="right" id="flowchart"></div>
                <div class="SocialMedia">
                    <i class="fa-brands fa-facebook-f"></i>
                    <i class="fa-brands fa-twitter"></i>
                    <i class="fa-brands fa-instagram"></i>
                    <i class="fa-brands fa-github"></i>
                </div>
            </div>
        </div>
		{:else if currentPage === 'about'}
        <div class="aboutbody">
            <h2>About Section</h2>
            <p>This is the about section content.</p>
            <button on:click={() => navigate('home')}>Back to Home</button>
        </div>
    {/if}
</div>

<style>
	.mainbody {
		width: 100%;
		height: 600px;
		background-image: url('Background2.png');
		background-size: cover;
	}

	.heading {
		display: flex;
		justify-content: space-evenly;
		padding-top: 65px;
		align-items: center;
		flex-wrap: wrap;
	}

	.right {
		width: 400px;
		height: 400px;
		background-image: url('flow-chart.gif');
		background-size: cover;
		border-radius: 50%;
		display: flex;
		justify-content: center;
		align-items: center;
		margin-top: 4.1%;
		margin-right: 3%;
		position: relative; 
	}

	.right::before {
		content: '';
		position: absolute;
		width: 420px; 
		height: 420px; 
		border: 2px solid white;
		border-radius: 50%;
		top: -10px; 
		left: -10px; 
	}

	/***left*****/
	.left p:nth-child(1) {
		color: orange;
		font-size: 30px;
		letter-spacing: 1px;
		font-style: italic;
		white-space: nowrap; 
		overflow: hidden;
		box-sizing: border-box;
		animation: marquee 15s linear infinite;
		margin-top: 2%;
	}
	.left p:nth-child(2) {
		color: white;
		font-size: 21px;
		letter-spacing: 1px;
		padding-top: 20px;
		padding-bottom: 15px;
	}
	.left h1 {
		font-size: 90px;
		color: white;
	}
	.left p:nth-child(3) {
		color: orange;
		font-size: 30px;
		font-style: italic;
		padding-bottom: 20px;
	}

	/****SocialMedia******/
	.SocialMedia {
		position: absolute;
		right: 11%;
		display: flex;
		justify-content: space-evenly;
		align-items: center;
		flex-direction: column;
		width: 40px;
		height: 200px;
		margin-top: 2%;
		background-color: white;
		font-size: 25px;
	}

	.SocialMedia i:hover {
		color: orange;
	}

	/*****letsmake****/

	.left button {
		width: 150px;
		height: 50px;
		font-size: 18px;
		border-radius: 20px;
		border: 2px solid white;
		background-color: transparent;
		color: white;
		margin: 20px 0px;
		position: relative;
		overflow: hidden;
		z-index: 1;
	}

	.left button::before {
		content: '';
		position: absolute;
		top: 0;
		left: -100%;
		width: 100%;
		height: 100%;
		background-color: orange;
		transition: left 0.4s ease;
		z-index: -1;
	}
	.left button:hover::before {
		left: 0;
	}
	.left button:hover {
		color: white;
	}

	
</style>