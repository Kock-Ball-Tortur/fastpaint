<script lang="ts">
  import Toolbar from "./lib/Toolbar.svelte"

  let imageArrived = false
  let imgSource = ""
  window.addEventListener("paste", async event => {
    event.preventDefault()
    try {
      const clipboardItems = await navigator.clipboard.read()
      console.log(clipboardItems)
      const blobOutput = await clipboardItems[0].getType("image/png")
      imgSource = window.URL.createObjectURL(blobOutput)
      imageArrived = true
    } catch {
      console.log("no worky :)")
    }
  })

  const fileInputChange = (event: Event) => {
    const target = event.target as HTMLInputElement
    const files = target.files

    imgSource = window.URL.createObjectURL(files[0])
    imageArrived = true
  }
</script>

<main>
  <Toolbar />
  <div id="imgContainer">
    <img src={imgSource} alt="" />
  </div>
  {#if !imageArrived}
    <label id="labelForUpload" for="testInput"> Upload an Image! </label>
    <input on:change={fileInputChange} id="testInput" type="file" accept="image/*" />
  {/if}
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
