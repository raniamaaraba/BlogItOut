<script>
  import './app.css';
  import Home from './home.svelte';
  import Projects from './projects.svelte';
  import Resume from './resume.svelte';
  import Me from './whoami.svelte';

  let route = location.pathname;

  function navigate(path) {
    history.pushState({}, '', path);
    route = path;
  }

  window.addEventListener('popstate', () => {
    route = location.pathname;
  });
</script>

{#if route === '/'}
  <Home {navigate} />
{:else if route === '/projects'}
  <Projects {navigate} />
{:else if route === '/resume'}
  <Resume {navigate} />
{:else if route === '/about'}
  <Me {navigate} />
{:else}
  <Home {navigate} />
{/if}