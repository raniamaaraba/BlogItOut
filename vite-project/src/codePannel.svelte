<script>
  import { onDestroy } from 'svelte';

  export let codeUrl = '';
  let codeOpen = false;
  let codeLoading = false;
  let codeText = '';
  let highlighted = '';
  let copied = false;
  let Prism = null;

  async function loadPrism() {
    if (Prism) return Prism;
    const mod = await import('prismjs');
    await import('prismjs/components/prism-cpp.js');
    Prism = mod.default ?? mod;
    return Prism;
  }

  async function loadCode() {
    if (!codeUrl || codeLoading || codeText) return;
    codeLoading = true;
    try {
      const res = await fetch(codeUrl);
      codeText = await res.text();
      await loadPrism();
      highlighted = Prism.highlight(codeText, Prism.languages.cpp, 'cpp');
    } catch (err) {
      codeText = '// Error loading code';
      highlighted = Prism ? Prism.highlight(codeText, Prism.languages.cpp, 'cpp') : codeText;
    } finally {
      codeLoading = false;
    }
  }

  function toggleCode() {
    codeOpen = !codeOpen;
    if (codeOpen) loadCode();
  }

  async function copyCode() {
    if (!codeText) return;
    await navigator.clipboard.writeText(codeText);
    copied = true;
    setTimeout(() => (copied = false), 1500);
  }

  onDestroy(() => {
    // placeholder for cleanup if needed later
  });
</script>

<div class="code-panel">
  <button class="toggle-code" on:click={toggleCode}>
    {codeOpen ? 'Hide source' : 'Show source'}
  </button>

  {#if codeOpen}
    {#if codeLoading}
      <div class="code-loading">Loading source…</div>
    {:else}
      <div class="code-toolbar">
        <button class="copy-btn" on:click={copyCode}>{copied ? 'Copied' : 'Copy'}</button>
        <a class="raw-link" href={codeUrl} target="_blank" rel="noopener noreferrer">Open raw</a>
      </div>

      <pre class="code-block"><code class="language-cpp">{@html highlighted}</code></pre>
    {/if}
  {/if}
</div>

<style>
  .code-panel { margin-top: 1rem; }
  .toggle-code { background: none; border: 2px solid #567; color: #567; padding: 0.4rem 0.8rem; border-radius: 6px; cursor: pointer; font-weight: 600; }
  .code-toolbar { display: flex; justify-content: flex-end; gap: 0.5rem; margin: 0.5rem 0; }
  .copy-btn { background: #0b2545; color: #fff; border: none; padding: 0.35rem 0.6rem; border-radius: 6px; cursor: pointer; }
  .raw-link { color: #0b2545; text-decoration: underline; align-self: center; }
  .code-block {
    background: #0f1724;
    color: #e6eef8;
    padding: 1rem;
    border-radius: 8px;
    overflow: auto;
    font-family: ui-monospace, SFMono-Regular, Menlo, Monaco, "Roboto Mono", monospace;
    font-size: 0.9rem;
    line-height: 1.45;
    max-height: 60vh;
  }
  .code-loading { color: #567; padding: 0.5rem 0; }
</style>
