<script>
  let x = "Basic",
    width = 300,
    height = 300,
    fliph = false,
    flipv = false,
    blur = 1,
    brightness = 10,
    contrast = 10,
    drop = 1,
    grayscale = 0,
    hue = 1,
    invert = 0,
    opacity = 10,
    saturate = 10,
    link = "",
    Thickness = 0,
    color = "#ff0000",
    type = "solid",
    bt_thickness = 0,
    bt_color = "#ff000",
    bt_type = "solid",
    br_thickness = 0,
    br_color = "#ff000",
    br_type = "solid",
    bb_thickness = 0,
    bb_color = "#ff000",
    bb_type = "solid",
    bl_thickness = 0,
    bl_color = "#ff000",
    bl_type = "solid",
    bt_open = false,
    br_open = false,
    bb_open = false,
    bl_open = false,
    btr = 0,
    btl = 0,
    bbr = 0,
    bbl = 0;
  function onChange(event, a) {
    if (a == 0) {
      type = event.currentTarget.value;
    } else if (a == 1) {
      bt_type = event.currentTarget.value;
    } else if (a == 2) {
      br_type = event.currentTarget.value;
    } else if (a == 3) {
      bb_type = event.currentTarget.value;
    } else if (a == 4) {
      bl_type = event.currentTarget.value;
    }
  }
  $: {
    console.log(type, bt_type);
  }
</script>

<header>
  <button on:click={() => (x = "Basic")}> Basic </button>
  <button on:click={() => (x = "Border")}> Frame </button>
  <button on:click={() => (x = "Rotate")}> Tools </button>
</header>

<div id="main">
  <section id="image">
    <section id="link">
      <h3>URL :</h3>
      <input bind:value={link} placeholder="Link of the image" />
    </section>

    <br /><br />
    <img
      src={link == ""
        ? "https://cdn2.thecatapi.com/images/9LKHhMRst.false"
        : link}
      {width}
      {height}
      alt="img to edit"
      style="
		transform: scale({flipv ? -1 : 1},{fliph
        ? -1
        : 1});
		filter: brightness({brightness / 10}) invert({invert /
        10}) saturate({saturate / 10}) contrast({contrast /
        10}) grayscale({grayscale / 10}) opacity({opacity /
        10});
		border : {Thickness}px {type} {color};
    border-top-width:{bt_thickness}px;
    border-top-style:{bt_type};
    border-top-color:{bt_color};
    border-right-width:{br_thickness}px;
    border-right-style:{br_type};
    border-right-color:{br_color};
        border-bottom-width:{bb_thickness}px;
    border-bottom-style:{bb_type};
    border-bottom-color:{bb_color};
        border-left-width:{bl_thickness}px;
    border-left-style:{bl_type};
    border-left-color:{bl_color};
border-top-right-radius: {btr}px;
border-top-left-radius: {btl}px;
border-bottom-right-radius: {bbr}px;
border-bottom-left-radius: {bbl}px;
		"
    />
  </section>
  <br />
  {#if x == "Basic"}
    <section id="items">
      <b> Width : </b><input bind:value={width} placeholder="Width" />
      <br />
      <b> Height : </b><input bind:value={height} placeholder="Height" />

      <div id="flip">
        <div>
          <b> Flip Vertically : </b><input
            type="checkbox"
            bind:checked={flipv}
          />
        </div>
        <div>
          <b> Flip Horizontally : </b><input
            type="checkbox"
            bind:checked={fliph}
          />
        </div>
      </div>
      <div class="ranges">
        <b>Brightness : </b>
        <input
          type="range"
          class="points"
          min="1"
          max="10"
          bind:value={brightness}
        />
      </div>

      <div class="ranges">
        <b>Saturaton : </b>
        <input
          type="range"
          class="points"
          min="0"
          max="10"
          bind:value={saturate}
        />
      </div>

      <div class="ranges">
        <b>Contrast : </b>
        <input
          type="range"
          class="points"
          min="0"
          max="10"
          bind:value={contrast}
        />
      </div>

      <div class="ranges">
        <b>GrayScale : </b>
        <input
          type="range"
          class="points"
          min="0"
          max="10"
          bind:value={grayscale}
        />
      </div>

      <div class="ranges">
        <b>Invert : </b>
        <input
          type="range"
          class="points"
          min="0"
          max="10"
          bind:value={invert}
        />
      </div>

      <div class="ranges">
        <b>Opacity : </b>
        <input
          type="range"
          class="points"
          min="0"
          max="10"
          bind:value={opacity}
        />
      </div>
    </section>
  {:else if x == "Border"}
    <section id="items">
      <div>
        <div
          style=" font-size: large;width:100%;display:flex;justify-content:space-between"
        >
          <h4>Top Side Frame</h4>
          <button
            on:click={() => {
              if (bt_open == false) {
                bt_open = true;
              } else {
                bt_open = false;
              }
            }}>{bt_open ? "Hide" : "Show"}</button
          >
        </div>
        {#if bt_open == true}
          <b>Thickness :</b> <br />
          <input
            type="number"
            placeholder="Thickness"
            bind:value={bt_thickness}
          />
          <br />
          <b>Type : </b><br />
          <div class="type">
            <label for="dotted">Dotted</label>
            <input
              type="radio"
              on:change={(e) => onChange(e, 1)}
              id="dotted"
              name="type"
              value="dotted"
            />
          </div>
          <div class="type">
            <label for="solid">Solid</label>
            <input
              type="radio"
              on:change={(e) => onChange(e, 1)}
              id="solid"
              name="type"
              value="solid"
            />
          </div>
          <div class="type">
            <label for="double">Double</label>
            <input
              type="radio"
              on:change={(e) => onChange(e, 1)}
              id="double"
              name="type"
              value="double"
            />
          </div>
          <div class="type">
            <label for="dashed">Dashed</label>
            <input
              type="radio"
              on:change={(e) => onChange(e, 1)}
              id="dashed"
              name="type"
              value="dashed"
            />
          </div>
          <div class="type">
            <label for="ridge">Ridge</label>
            <input
              type="radio"
              on:change={(e) => onChange(e, 1)}
              id="ridge"
              name="type"
              value="ridge"
            />
          </div>
          <div class="type">
            <label for="outset">Outset</label>
            <input
              type="radio"
              on:change={(e) => onChange(e, 1)}
              id="outset"
              name="type"
              value="outset"
            />
          </div>
          <div class="type">
            <label for="inset">Inset</label>
            <input
              type="radio"
              on:change={(e) => onChange(e, 1)}
              id="inset"
              name="type"
              value="inset"
            />
          </div>
          <b>Color :</b><br />
          <input type="color" bind:value={bt_color} />
        {/if}
      </div>
      <br />
      <div>
        <div
          style=" font-size: large;width:100%;display:flex;justify-content:space-between"
        >
          <h4>Right Side Frame</h4>
          <button
            on:click={() => {
              if (br_open == false) {
                br_open = true;
              } else {
                br_open = false;
              }
            }}>{br_open ? "Hide" : "Show"}</button
          >
        </div>
        {#if br_open == true}
          <b>Thickness :</b> <br />
          <input
            type="number"
            placeholder="Thickness"
            bind:value={br_thickness}
          />
          <br />
          <b>Type : </b><br />
          <div class="type">
            <label for="dotted">Dotted</label>
            <input
              type="radio"
              on:change={(e) => onChange(e, 2)}
              id="dotted"
              name="type"
              value="dotted"
            />
          </div>
          <div class="type">
            <label for="solid">Solid</label>
            <input
              type="radio"
              on:change={(e) => onChange(e, 2)}
              id="solid"
              name="type"
              value="solid"
            />
          </div>
          <div class="type">
            <label for="double">Double</label>
            <input
              type="radio"
              on:change={(e) => onChange(e, 2)}
              id="double"
              name="type"
              value="double"
            />
          </div>
          <div class="type">
            <label for="dashed">Dashed</label>
            <input
              type="radio"
              on:change={(e) => onChange(e, 2)}
              id="dashed"
              name="type"
              value="dashed"
            />
          </div>
          <div class="type">
            <label for="ridge">Ridge</label>
            <input
              type="radio"
              on:change={(e) => onChange(e, 2)}
              id="ridge"
              name="type"
              value="ridge"
            />
          </div>
          <div class="type">
            <label for="outset">Outset</label>
            <input
              type="radio"
              on:change={(e) => onChange(e, 2)}
              id="outset"
              name="type"
              value="outset"
            />
          </div>
          <div class="type">
            <label for="inset">Inset</label>
            <input
              type="radio"
              on:change={(e) => onChange(e, 2)}
              id="inset"
              name="type"
              value="inset"
            />
          </div>
          <b>Color :</b><br />
          <input type="color" bind:value={br_color} />
        {/if}
      </div>
      <br />
      <diV>
        <div
          style=" font-size: large;width:100%;display:flex;justify-content:space-between"
        >
          <h4>Bottom Side Frame</h4>
          <button
            on:click={() => {
              if (bb_open == false) {
                bb_open = true;
              } else {
                bb_open = false;
              }
            }}>{bb_open ? "Hide" : "Show"}</button
          >
        </div>
        {#if bb_open == true}
          <b>Thickness :</b> <br />
          <input
            type="number"
            placeholder="Thickness"
            bind:value={bb_thickness}
          />
          <br />
          <b>Type : </b><br />
          <div class="type">
            <label for="dotted">Dotted</label>
            <input
              type="radio"
              on:change={(e) => onChange(e, 3)}
              id="dotted"
              name="type"
              value="dotted"
            />
          </div>
          <div class="type">
            <label for="solid">Solid</label>
            <input
              type="radio"
              on:change={(e) => onChange(e, 3)}
              id="solid"
              name="type"
              value="solid"
            />
          </div>
          <div class="type">
            <label for="double">Double</label>
            <input
              type="radio"
              on:change={(e) => onChange(e, 3)}
              id="double"
              name="type"
              value="double"
            />
          </div>
          <div class="type">
            <label for="dashed">Dashed</label>
            <input
              type="radio"
              on:change={(e) => onChange(e, 3)}
              id="dashed"
              name="type"
              value="dashed"
            />
          </div>
          <div class="type">
            <label for="ridge">Ridge</label>
            <input
              type="radio"
              on:change={(e) => onChange(e, 3)}
              id="ridge"
              name="type"
              value="ridge"
            />
          </div>
          <div class="type">
            <label for="outset">Outset</label>
            <input
              type="radio"
              on:change={(e) => onChange(e, 3)}
              id="outset"
              name="type"
              value="outset"
            />
          </div>
          <div class="type">
            <label for="inset">Inset</label>
            <input
              type="radio"
              on:change={(e) => onChange(e, 3)}
              id="inset"
              name="type"
              value="inset"
            />
          </div>
          <b>Color :</b><br />
          <input type="color" bind:value={bb_color} />
        {/if}
      </diV>
      <br />
      <diV>
        <div
          style=" font-size: large;width:100%;display:flex;justify-content:space-between"
        >
          <h4>Left Side Frame</h4>
          <button
            on:click={() => {
              if (bl_open == false) {
                bl_open = true;
              } else {
                bl_open = false;
              }
            }}>{bl_open ? "Hide" : "Show"}</button
          >
        </div>
        {#if bl_open == true}
          <b>Thickness :</b> <br />
          <input
            type="number"
            placeholder="Thickness"
            bind:value={bl_thickness}
          />
          <br />
          <b>Type : </b><br />
          <div class="type">
            <label for="dotted">Dotted</label>
            <input
              type="radio"
              on:change={(e) => onChange(e, 4)}
              id="dotted"
              name="type"
              value="dotted"
            />
          </div>
          <div class="type">
            <label for="solid">Solid</label>
            <input
              type="radio"
              on:change={(e) => onChange(e, 4)}
              id="solid"
              name="type"
              value="solid"
            />
          </div>
          <div class="type">
            <label for="double">Double</label>
            <input
              type="radio"
              on:change={(e) => onChange(e, 4)}
              id="double"
              name="type"
              value="double"
            />
          </div>
          <div class="type">
            <label for="dashed">Dashed</label>
            <input
              type="radio"
              on:change={(e) => onChange(e, 4)}
              id="dashed"
              name="type"
              value="dashed"
            />
          </div>
          <div class="type">
            <label for="ridge">Ridge</label>
            <input
              type="radio"
              on:change={(e) => onChange(e, 4)}
              id="ridge"
              name="type"
              value="ridge"
            />
          </div>
          <div class="type">
            <label for="outset">Outset</label>
            <input
              type="radio"
              on:change={(e) => onChange(e, 4)}
              id="outset"
              name="type"
              value="outset"
            />
          </div>
          <div class="type">
            <label for="inset">Inset</label>
            <input
              type="radio"
              on:change={(e) => onChange(e, 4)}
              id="inset"
              name="type"
              value="inset"
            />
          </div>
          <b>Color :</b><br />
          <input type="color" bind:value={bl_color} />
        {/if}
      </diV>
    </section>
  {:else}
    <section id="items">
      <b> Top-Right Radius [Bend] :</b><input
        bind:value={btr}
        placeholder="Width"
      />

      <b> Top-Left-Radius [Bend] :</b><input
        bind:value={btl}
        placeholder="Height"
      />
      <b> Bottom-Right-Radius [Bend] :</b><input
        bind:value={bbr}
        placeholder="Width"
      />

      <b>Bottom-Left-Radius [Bend]:</b><input
        bind:value={bbl}
        placeholder="Height"
      />
    </section>
  {/if}
</div>

<style>
  header {
    height: 100px;
    display: flex;
    justify-content: center;
    align-items: center;
  }
  .type {
    width: 100%;
    display: flex;
    justify-content: space-between;
  }
  button {
    color: crimson;
    background: none;
    margin-left: 20px;
    margin-right: 20px;
    border: none;
    font-size: large;
  }
  button:hover {
    border-bottom: 2px solid rgba(0, 0, 0, 0.5);
  }
  button:focus {
    background: none;
    border: 2px solid rgba(0, 0, 0, 0.5);
  }
  #items {
    width: 95vw;
    margin: 0;
    margin-left: 3vw;
  }
  #main {
    margin: 0;
    width: 90vw;
    display: flex;
    flex-direction: column;
    align-items: center;
    margin-left: 8vw;
  }
  input::placeholder {
    text-align: center;
  }
  #flip {
    width: 100%;
    display: flex;
    justify-content: space-around;
    align-items: center;
  }
  .ranges {
    display: flex;
    width: 100%;
    justify-content: space-around;
    align-items: center;
  }
  #link {
    width: 100%;
    display: flex;
    justify-content: center;
    vertical-align: middle;
  }
  #link input {
    margin-left: 20px;
    border: none;
    border-bottom: 2px solid black;
  }
  #flip {
    flex-direction: column;
  }
  @media only screen and (min-width: 800px) {
    #main {
      display: flex;
      flex-direction: row-reverse;
      width: 100vw;
      margin: 0;
      padding: 0;
      justify-content: space-evenly;
      align-items: baseline;
    }
    #link {
      margin-bottom: auto;
      height: fit-content;
    }
    .ranges {
      display: flex;
      justify-content: space-between;
      flex-direction: column;
      margin-right: 100px;
    }
    #items {
      padding: 20px;
      display: flex;
      flex-direction: column;
      justify-content: center;
      border: 2px solid crimson;
      width: 20vw;
      box-shadow: 5px 10px 8px 10px #888888;
      padding-bottom: 0;
    }
  }
</style>
