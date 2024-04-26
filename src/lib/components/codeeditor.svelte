<script lang="ts">
  import { onDestroy, onMount } from "svelte";

  // Monaco deps and declarations
  import type * as Monaco from 'monaco-editor/esm/vs/editor/editor.api'
  let editor: Monaco.editor.IStandaloneCodeEditor;
  let monaco: typeof Monaco;
  let editorContainer: HTMLElement;

  onMount(async () => {
    // Import monaco
    monaco = (await import('$lib/monaco')).default;
    const editor = monaco.editor.create(editorContainer);
    const model = monaco.editor.createModel("print(\"Hello World!\")", "python");
    editor.setModel(model);
  });

  onDestroy(() => {
    monaco?.editor.getModels().forEach((model) => model.dispose());
    editor?.dispose();
  });
</script>

<div class="editor" bind:this={editorContainer}></div>

<style>
  .editor {
    width: 100%;
    height: 100%;
  }
</style>