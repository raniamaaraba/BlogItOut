<script>
  export let navigate = (p) => (location.pathname = p);

  let projects = [
    {
      id: 1,
      title: "Flight Control System",
      preview: "Embedded C++ modules for aerospace safety...",
      content: "In this project, I developed flight control software for an aerospace system. I focused on safety-critical embedded C++ modules, collaborating with engineers to ensure precision and reliability."
    },
    {
      id: 2,
      title: "Portfolio Website",
      preview: "Responsive bilingual site built with Svelte/Tailwind...",
      content: "I designed and implemented a responsive portfolio site with an ENG/日本語 toggle. It uses Svelte and TailwindCSS for clean layouts, branded navigation, and polished visuals."
    },
    {
      id: 3,
      title: "Kanji Learning Tool",
      preview: "Interactive UI for studying kanji roots...",
      content: "This project combines my love for language and software. I built an interactive tool to explore kanji anatomy, with hover effects, tooltips, and responsive design."
    }
  ];

  let expanded = null;
  function toggleProject(id) {
    expanded = expanded === id ? null : id;
  }
</script>

<main class="container">
  <!-- Header -->
  <header class="projects-header">
    <div class="header-bar">
      <h1 class="title">Projects</h1>
      <nav class="nav">
        <a href="/" on:click|preventDefault={() => navigate('/')}>Home</a>
        <a href="/about" on:click|preventDefault={() => navigate('/about')}>About</a>
        <a href="/projects" on:click|preventDefault={() => navigate('/projects')}>Projects</a>
        <a href="/resume" on:click|preventDefault={() => navigate('/resume')}>Resume</a>
      </nav>
    </div>
    <p class="subtitle">Wanna learn more? Click one to find out!</p>
  </header>

  <!-- Project list OR focused project -->
  {#if expanded === null}
    <section class="projects">
      <div class="project-list">
        {#each projects as project}
          <article class="project-card" on:click={() => toggleProject(project.id)}>
            <h3>{project.title}</h3>
            <p class="preview">{project.preview}</p>
          </article>
        {/each}
      </div>
    </section>
  {:else}
    <section class="project-focus">
      <button class="back-btn" on:click={() => (expanded = null)}>← Back to Projects</button>
      <h2>{projects.find(p => p.id === expanded).title}</h2>
      <p>{projects.find(p => p.id === expanded).content}</p>
    </section>
  {/if}
</main>

<style>
  /* Header bar consistent with Home */
  .header-bar {
    display: flex;
    justify-content: space-between;
    align-items: center;
    flex-wrap: wrap;
    gap: 1rem;
  }

  .title {
    font-family: 'Imperial Script', cursive;
    font-size: 3.5rem;
    margin: 0;
    color: #0b2545;
  }

  .subtitle {
    font-size: 1.2rem;
    color: #567;
    margin-top: 0.5rem;
  }

  .nav {
    display: flex;
    gap: 1.5rem;
    font-weight: 500;
  }

  .nav a {
    color: #567;
    text-decoration: none;
  }

  .nav a:hover {
    text-decoration: underline;
  }

  /* Project list */
  .project-list {
    display: flex;
    flex-direction: column;
    gap: 1.5rem;
  }

  .project-card {
    border: 1px solid #ddd;
    border-radius: 8px;
    padding: 1rem;
    background: #fafafa;
    cursor: pointer;
    transition: background 0.2s ease;
  }

  .project-card:hover {
    background: #f0f0f0;
  }

  .project-card h3 {
    margin: 0;
    font-size: 1.3rem;
    color: #567;
  }

  .preview {
    color: #334155;
    margin-top: 0.5rem;
  }

  /* Focused project view */
  .project-focus {
    margin-top: 2rem;
    padding: 1.5rem;
    border: 1px solid #ddd;
    border-radius: 8px;
    background: #fff;
  }

  .project-focus h2 {
    font-size: 2rem;
    margin-bottom: 1rem;
    color: #0b2545;
  }

  .project-focus p {
    color: #444;
    line-height: 1.6;
  }

  .back-btn {
    background: none;
    border: 2px solid #567;
    color: #567;
    padding: 0.4rem 1rem;
    border-radius: 6px;
    cursor: pointer;
    font-weight: 600;
    margin-bottom: 1rem;
  }

  .back-btn:hover {
    background: #f0f0f0;
  }
</style>
