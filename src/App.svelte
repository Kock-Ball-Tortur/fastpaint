<script lang="ts">
let getTextTest: string
  navigator.clipboard
    .readText()
    .then(clipText => getTextTest = clipText)
</script>

<main>
  <div id="imgContainer">
    <p>{getTextTest}</p>
  </div>
</main>

<style>
</style>
