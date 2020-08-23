<script>
  import getCoordinates from "./getCoordinates"

  let isOpen = false

  let textarea

  let coordinates = { top: 0, left: 0 }

  export let minHeight = "100px"

  export let trigger = "@"

  export let value = ""

  export let disabled = false

  export let readonly = false

  export let placeholder = ""

  $: console.log(coordinates)

  const handleKeyUp = (evt) => {}

  const handleChange = () => setCoodinates()

  const setCoodinates = () => {
    const { left, top } = getCoordinates(textarea, textarea.selectionEnd)

    let nextTop = top

    if (textarea.scrollHeight > textarea.clientHeight) {
      nextTop = top - (textarea.scrollHeight - textarea.clientHeight)
    }

    coordinates = { left, top: nextTop }
  }
</script>

<style>
  .wrapper {
    position: relative;
  }
  pre {
    width: 100%;
    height: 100%;
    color: transparent;
    border: none;
    box-sizing: border-box;
    color: transparent;
    white-space: pre-wrap;
    word-wrap: break-word;
    z-index: 1000;
  }
  textarea {
    width: 100%;
    height: 100%;
    position: absolute;
    top: 0;
    left: 0;
    z-index: 1200;
    overflow: hidden;
  }

  pre,
  textarea {
    font-family: inherit;
    color: inherit;
  }
</style>

<div class="wrapper" style="min-height: {minHeight}">
  <pre>{value}</pre>
  <textarea
    bind:this={textarea}
    bind:value
    {disabled}
    {readonly}
    {placeholder}
    on:paste={handleChange}
    on:input={handleChange} />
</div>
