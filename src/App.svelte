<script lang="ts">
  import Toolbar from "./lib/Toolbar.svelte"

  let imageArrived = false
  let imgSource = ""
  // this will turn the image to a canvas to be able to work with it using Canvas API
  function imageToCanvas() {
    let canvas = document.querySelector("#imgToCanvas") as HTMLCanvasElement
    let context = canvas.getContext("2d")
    let img = document.createElement("img") //creating an imageelement to draw from
    img.src = imgSource
    // not to happy about   using onload in l14 but i am sick and i dont want to do better right now fuck you
    // eslint-disable-next-line unicorn/prefer-add-event-listener
    img.onload = () => {
      //draw image onto canvas as soon as it is loaded
      canvas.width = img.width // resize canvas to image size
      canvas.height = img.height
      context.drawImage(img, 0, 0)
    }
  }
  //Used to paste Images
  window.addEventListener("paste", async event => {
    event.preventDefault()
    try {
      const clipboardItems = await navigator.clipboard.read()
      console.log(clipboardItems)
      const blobOutput = await clipboardItems[0].getType("image/png")
      imgSource = window.URL.createObjectURL(blobOutput)
      imageArrived = true
      imageToCanvas()
    } catch {
      console.log("no worky :)")
    }
  })
  //Used to insert images utilizing file browser
  const fileInputChange = (event: Event) => {
    const target = event.target as HTMLInputElement
    const files = target.files

    imgSource = window.URL.createObjectURL(files[0])
    imageArrived = true
    imageToCanvas()
  }
</script>

<main>
  {#if !imageArrived}
    <label id="labelForUpload" for="testInput"> Upload an Image! </label>
    <input on:change={fileInputChange} id="testInput" type="file" accept="image/*" />
  {:else}
    <Toolbar />
  {/if}
  <div id="imgContainer">
    <canvas id="imgToCanvas" />
  </div>
</main>

<style lang="scss">
  #testInput {
    display: none;
  }

  #labelForUpload {
    border: 1px solid #ccc;
    border-radius: 5px;
    display: inline-block;
    padding: 6px 12px;
    cursor: pointer;

    &:active {
      background-color: rgb(231, 231, 231);
    }
  }
</style>
