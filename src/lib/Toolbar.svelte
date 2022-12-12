<script>
  import Draw from "./Tools/Draw.svelte"
  import Cut from "./Tools/Cut.svelte"
</script>

<div id="toolbar">
  <Draw />
  <Cut />
</div>

<style lang="scss">
  #toolbar {
    display: inline-flex;
  }
</style>
