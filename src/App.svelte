<script lang="ts">
  let img: string
  window.addEventListener("paste", async event => {
    event.preventDefault()
    try {
      const clipboardItems = await navigator.clipboard.read()
      console.log(clipboardItems)
      const blobOutput = await clipboardItems[0].getType("image/png")
      img = window.URL.createObjectURL(blobOutput)
    } catch {
      console.log("no worky :)")
    }
  })
</script>

<main>
  <div id="imgContainer">
    <img src={img} alt="Paste Image" />
  </div>
</main>

<style>
</style>
