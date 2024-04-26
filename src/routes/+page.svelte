<script lang="ts">
  import CodeEditor from "$lib/components/codeeditor.svelte";
</script>

<div class="page-content">
  <img src="icons/algo-logo.svg" alt="algo-logo" class="main-algo-logo"/>
  <div class="code-editor-holder">
    <CodeEditor language="python" theme="Monokai"/>
  </div>
</div>

<style>
  .page-content {
    display: flex;
    justify-content: center;
    align-items: center;
    flex-flow: column nowrap;
  }
  .main-algo-logo {
    margin-top: 10%;
    width: 20%;
    aspect-ratio: 1 / 1;
  }
  .code-editor-holder {
    width: 75%;
    height: 20rem;
  }
</style>