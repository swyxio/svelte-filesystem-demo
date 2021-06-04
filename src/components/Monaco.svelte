<script>
    import { onMount, onDestroy } from 'svelte'
    import * as monaco from 'monaco-editor';
    let editor
    onMount(mountEditor)
    function mountEditor() {
        editor = monaco.editor.create(document.getElementById('monaco-container'), {
          value: [
            'function x() {',
            '\tconsole.log("Hello world!");',
            '}'
          ].join('\n'),
          language: 'css',
        });
    }
    onDestroy(() => {
      if (editor) {
        editor.dispose();
        const model = editor.getModel();
        if (model) model.dispose();
      }
    })
  </script>
  
  <style>
    #monaco-container {
      height: 40vh;
      width: 40vw;
      min-width: 600px;
      position: fixed;
      z-index: 999;
      bottom: 0;
      left: 0;
    }
  </style>
  <div id="monaco-container"></div>