
<script>
  import { onMount } from 'svelte';
  import { marked } from 'marked';
  import hljs from 'highlight.js';
  let markdown = '# stupidmarkdown\n\nStart typing your Markdown on the left.';
  let html = '';
  let dark = true;

  // Configure marked to use highlight.js for code blocks (let marked handle escaping)
  marked.setOptions({
    highlight: function(code, lang) {
      if (lang && hljs.getLanguage(lang)) {
        return hljs.highlight(code, { language: lang }).value;
      }
      return hljs.highlightAuto(code).value;
    }
  });

  function updatePreview() {
    html = marked.parse(markdown);
  }

  function toggleTheme() {
    dark = !dark;
    document.documentElement.setAttribute('data-theme', dark ? 'dark' : 'light');
  }

  onMount(() => {
    updatePreview();
    document.documentElement.setAttribute('data-theme', dark ? 'dark' : 'light');
  });
</script>

<main class="container">
  <div class="theme-toggle">
    <button on:click={toggleTheme} aria-label="Toggle dark/light mode">
      {dark ? '🌙' : '☀️'}
    </button>
  </div>
  <div class="editor-preview">
    <section class="editor">
      <textarea
        bind:value={markdown}
        on:input={updatePreview}
        spellcheck="false"
        aria-label="Markdown editor"
      ></textarea>
    </section>
    <div class="divider"></div>
    <section class="preview">
      <div class="markdown-body">{@html html}</div>
    </section>
  </div>
</main>

<style>
  :global(:root) {
    --bg: #f8fafc;
    --fg: #222;
    --border: #e5e7eb;
    --editor-bg: #f1f5f9;
    --preview-bg: #fff;
    --accent: #6366f1;
    --divider: #e0e7ef;
    --radius: 1.5rem;
    --pane-radius: 1.2rem;
    --pane-padding: 2.2rem;
  }
  :global([data-theme='dark']) {
    --bg: #18181b;
    --fg: #f4f4f5;
    --border: #27272a;
    --editor-bg: #23272f;
    --preview-bg: #18181b;
    --accent: #818cf8;
    --divider: #23272f;
  }
  :global(body), :global(html) {
    background: var(--bg);
    color: var(--fg);
    margin: 0;
    padding: 0;
    font-family: system-ui, sans-serif;
    height: 100%;
    width: 100%;
  }
  .container {
    min-height: 100vh;
    background: var(--bg);
    color: var(--fg);
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: flex-start;
    padding: 2rem 0;
  }
  .theme-toggle {
    width: 100%;
    display: flex;
    justify-content: flex-end;
    margin-bottom: 1rem;
    padding-right: 2rem;
  }
  .theme-toggle button {
    background: var(--editor-bg);
    color: var(--fg);
    border: 1px solid var(--border);
    border-radius: 1rem;
    font-size: 1.2rem;
    padding: 0.4em 0.8em;
    cursor: pointer;
    transition: background 0.2s, color 0.2s;
    box-shadow: 0 2px 8px 0 rgba(0,0,0,0.04);
  }
  .editor-preview {
    display: flex;
    flex-direction: row;
    width: 1100px;
    max-width: 98vw;
    min-height: 70vh;
    background: var(--border);
    border-radius: var(--radius);
    overflow: hidden;
    box-shadow: 0 4px 32px 0 rgba(0,0,0,0.08);
  }
  .editor {
    flex: 1;
    background: var(--editor-bg);
    display: flex;
    flex-direction: column;
    border-top-left-radius: var(--pane-radius);
    border-bottom-left-radius: var(--pane-radius);
    padding: var(--pane-padding);
    overflow-y: auto;
  }
  .divider {
    width: 2px;
    background: var(--divider);
    margin: 0 0.5rem;
    border-radius: 1rem;
  }
  .preview {
    flex: 1;
    background: var(--preview-bg);
    overflow-y: auto;
    padding: var(--pane-padding);
    display: block;
    border-top-right-radius: var(--pane-radius);
    border-bottom-right-radius: var(--pane-radius);
    text-align: left;
  }
  textarea {
    flex: 1;
    width: 100%;
    background: var(--editor-bg);
    color: var(--fg);
    border: none;
    resize: none;
    font-size: 1.1em;
    font-family: 'JetBrains Mono', 'Fira Mono', 'Menlo', monospace;
    padding: 0;
    outline: none;
    border-radius: 0.7rem;
    box-shadow: 0 1px 4px 0 rgba(0,0,0,0.03);
  }
  .markdown-body {
    max-width: 48em;
    margin: 0;
    line-height: 1.6;
    color: var(--fg);
    font-size: 1.05em;
    word-break: break-word;
    text-align: left;
    align-items: flex-start;
    display: flex;
    flex-direction: column;
  }
  .markdown-body img {
    max-width: 100%;
    height: auto;
    display: block;
    margin: 1.5em auto;
    border-radius: 0.7em;
    box-shadow: 0 2px 8px 0 rgba(0,0,0,0.06);
  }
  .markdown-body pre code.hljs {
    display: block;
    overflow-x: auto;
    padding: 1em;
    border-radius: 0.5em;
    font-size: 1em;
    font-family: 'JetBrains Mono', 'Fira Mono', 'Menlo', monospace;
    text-align: left;
  }
</style>
