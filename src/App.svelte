<script lang="ts">
  let pastedImg = ""
  window.addEventListener("paste", async event => {
    event.preventDefault()
    try {
      const clipboardItems = await navigator.clipboard.read()
      console.log(clipboardItems)
      const blobOutput = await clipboardItems[0].getType("image/png")
      pastedImg = window.URL.createObjectURL(blobOutput)
    } catch {
      console.log("no worky :)")
    }
  })
</script>

<main>
  <div id="imgContainer">
    <img src={pastedImg} alt="" />
  </div>
</main>

<style>
</style>
