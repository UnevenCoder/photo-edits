<script>
let x='Basic', width=100,height=100,fliph=false,flipv=false,blur=1,brightness=1,contrast=1,drop=1
,grayscale=0,hue=1,invert=1,opacity=10,saturate=1

</script>
<style>
header{
	height:100px;
	display:flex;
	justify-content:center;
	align-items: center;
}
button{
	color:crimson;
	background: none;
	margin-left: 20px;
	margin-right: 20px;
	border:none;
	font-size: large;
}
button:hover{
	border-bottom:2px solid rgba(0,0,0,0.5);
	transform: scale(1.2)
	
}
button:focus{
	background:none;
	border:2px solid rgba(0,0,0,0.5);
	transform: scale(1.2)
}
#main{
	margin:0;
	width:90vw;
	display:flex;
	flex-direction: column;
	align-items: center;
	margin-left:8vw;
}
input::placeholder{
	text-align:center;
}
#flip{
	width:100%;
	display:flex;
    justify-content: space-around;
	align-items: center;
}
.ranges{
	display:flex;
	width:100%;
	justify-content: space-around;
	align-items: center;
}
</style>

<header>
	<button on:click={()=>x='Basic'}> Basic </button>
	<button on:click={()=>x='Border'}> Borders </button>
	<button on:click={()=>x='Rotate'}> Rotate </button>
</header>

<div id='main'>
	<section id='image'>
		<img src='https://cdn2.thecatapi.com/images/9LKHhMRst.false' 
		width={width} 
		height={height} 
		alt='img to edit' 
		style="
		transform: scale({flipv?-1:1},{fliph?-1:1});
		filter: brightness({brightness}) invert({invert}) saturate({saturate}) contrast({contrast}) grayscale({grayscale}) opacity({opacity})
		"/>
	</section>
	<br>
	{#if x == 'Basic'}
	<section>
		<b> Width : </b><input bind:value={width} placeholder='Width'/>
		<b> Height : </b><input bind:value={height} placeholder='Height'/>
		<br><br>
		<div id='flip'>
			<div>
		<b> Flip Vertically   :  </b><input type='checkbox' bind:checked={flipv} />
		</div>
		<div>
		<b> Flip Horizontally :  </b><input  type='checkbox' bind:checked={fliph}/>
		</div>

	</div>

	<br>
<div class='ranges'>
	<b>Brightness : </b> <input type="range" class="points"  min="1" max="10" bind:value={brightness}>
	</div>
	<br>
	<div class='ranges'>
	<b>Saturaton : </b> <input type="range" class="points"  min="1" max="10" bind:value={saturate}>
	</div>
	<br>
	<div class='ranges'>
	<b>Contrast : </b> <input type="range" class="points"  min="1" max="10" bind:value={contrast}>
	</div>
	<br>
	<div class='ranges'>
	<b>GrayScale : </b> <input type="range" class="points"  min="0" max="10" bind:value={grayscale}>
	</div>
	<br>
	<div class='ranges'>
	<b>Invert : </b> <input type="range" class="points"  min="0" max="10" bind:value={invert}>
		</div>
		<br>
	<div class='ranges'>
	<b>Opacity : </b> <input type="range" class="points"  min="1" max="10" bind:value={opacity}>
    </div>
			<br>

	<br>
	<br>

	</section>
	{:else if x=='Border'}
   <section>



   </section>
	{:else}

	<p>Other</p>
	{/if}
</div>