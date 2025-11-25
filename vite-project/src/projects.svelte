<script>
  import { onMount } from 'svelte';
  import CodePanel from './codePannel.svelte';
  export let navigate = (p) => (location.pathname = p);

  /* -------------------------
     Project images (import your assets)
     ------------------------- */
  import thumb1 from './assets/hartydarty/IMG_2250.jpeg';
  import img1a from './assets/hartydarty/DSC06724.jpg';
  import img1b from './assets/hartydarty/DSC06780.jpg';
  import img1c from './assets/hartydarty/DSC06782.jpg';
  import img1d from './assets/hartydarty/DSC06786.jpg';
  import img1e from './assets/hartydarty/DSC06786.jpg';
  import img1f from './assets/hartydarty/DSC06795.jpg';
  import img1g from './assets/hartydarty/DSC06829.jpg';

  import img2a from './assets/l2/cad.png';
  import img2b from './assets/l2/fails.jpg';
  import img2c from './assets/l2/IMG_1875.jpeg';
  import img2d from './assets/l2/openrocket.png';

  import thumb3 from './assets/r.jpeg';
  import img3a from './assets/IMG_2259.jpeg';

  // add more imports as needed

  /* -------------------------
     Project data (rich fields)
     ------------------------- */
  let projects = [
    {
      id: 1,
      title: "Flight Control System",
      role: "Avionics Team Member - Developer",
      date: "Sept 2025 – Dec 2025",
      tags: ["Aerospace", "Embedded Systems", "C++", "Avionics", "Rocketry"],
      tech: ["C++", "PlatformIO", "Git"],
      preview: "Avionics development for the Univeristy of Cincinnati's Rocketry Club's Boosted Dart",
      content: [
        "Developed along side colleagues Loring Teuteuberg and Jesse Dominguez (Avionics Lead) to create custom code for the avionics bay utilising PlatformIO in VSC with Adafruit LSM6DS, barometer MS5611 SPI on a Seeed ESP32S3.",
        "Main responsibilities included designing the control architecture, implementing sensor filtering and logging, and developing clean code for reusability",
        "Harty Darty was a large group effor by UCRO to create a boosted dart with Mach 1 capabilities. The goals of the avionics team was to create a fully custom avionics as well as an additional fall-back bay using the Blue Raven developed by Featherweight Altimiters. Harty Darty had a semi-sucessful launch on November 23nd with a delayed separation stage (it is important to know ths is a boosted dart, so the second stage did not contain a motor and was purily thrusted by the intial thrust and drag separation). ",
        "Being the second avionics project I've had the opportunity to work on, it was very rewarding to see the final project yet very difficult encoutering unknown waters. Majority of my projects have been local apps and website so encorperating hardware was pretty much entierly new to me as well as understanding fundamentals of electroncis and enacted forces. I have learned a lot more about hardware and software development incoorperation, CAD, wiring, working with a team for the greater good."
      ],
      bullets: [
        "Created a localhost through the Seeeed to allow the retrival of flight-logged data in a txt file",
        "Integrated IMU and barometer data with Kalman filtering",
        "Helped develop check tests to ensure continuity"
      ],
      links: [
        { label: "GitHub repo", href: "https://github.com/raniamaaraba/HardyDarty", external: true },
        { label: "Video comming soon!", href: "https://youtu.be/your-demo", external: true }
      ],
      thumb: thumb1,
      images: [ img1g, img1a, img1b, thumb1, img1c, img1d, img1e, img1f],
    },

    {
      id: 2,
      title: "Level 2 Certification Rocket", 
      role: "Avionics and Structures",
      date: "Sept 2025 - Present",
      tags: ["Rocketry", "Avionics","Hardware"],
      tech: ["Fusion360", "Open Rocket"],
      preview: "Creating my Level 2 certification rocket",
      content: [
        "Under mentorship of Landry Danielson, current Level 2 Tripoli and UCRO President, I set a goal to gain my Level 2 certification to gain a deeper knowledge of high powered rocketry as well as avionics development and aerospace community.",
        "Using a 4 in diamater on a J-800 motor, the Open Rocket simulation is predicted for the rocket to achieve an apogee of 4,900ft with a max velocity of over 1,000 ft/s. The entire rocket except for the fins are made of re-enforced cardboard with a 3D printed custom avionics bay.",
        "Currently looking to launch at the beginning of December--and have had many trials and tribulations along the way! After achieving my Jr Level 1 (now just Level 1) back in the fall of 2021, there was quite a bit I needed to re-learn about development of a new rocket with an unfamiliar matieral. Unlike my time previously working on our Harty Darty Rocket (go read it!!), my avionics bay this time was completely on my own and luckily was loaned components from the club to use. Although I have previously worked on physical impelemntation with a breadboard and understanding the fundamentals of wiring, this proved to be still a skill I want to work harder at with my lack of understanding and efficency. In addition, developing a electronics bay using Fusion 360 was entirely new and as I am sure Landry could atest, I am quite poor at. Half of the journey is learning what you don't know and this was a beautiful example of new skills that I want to improve on."
      ],
      bullets: [
        "Developing stable rockets in Open Rocket",
        "Created custom Avionics with modeling in Fusion360",
        "Learning and working with hardware",
        "Understanding the qualifications for a Level 2 capable rocket",
        "Grasping a larger understanding of better saftey protocols"
      ],
      thumb: img2c,
      images: [img2d, img2a, img2b, img2c],
    },

    {
      id: 3,
      title: "Portfolio Website",
      role: "Full Stack Developer",
      date: "Oct 2025 – Present",
      tags: ["Web Development", "Svelte", "Design"],
      tech: ["Svelte", "Tailwind", "NPM Packages", "Git Pages"],
      preview: "A comprehensive website to showcase projects, full resume, and humility of programming",
      content: [
        "A bilingual portfolio site to have a more indepth area to showcase and explain my current projects! Goal was to make an interactive website using Svelte to integrate a resume as well as characteristics of myself into one website.",
        "Focuses on responsive layout, Japanese and English content, and a small, fast bundle. "
      ],
      bullets: [
        "Created website from scratch using Svelte and Vite",
        "Implemented a projects feed with thumbnails and focused views",
        "Built a language toggle button with persisted preference.",
        "Learned more about embedding of media: images, video, and code"
      ],
      links: [
        { label: "This website!", href: "https://your-site.example", external: true }
      ],
      thumb: thumb3,
      images: [img3a]
    },

  ];

  /* -------------------------
     UI state
     ------------------------- */
  let expanded = null; // id of open project
  $: selected = projects.find(p => p.id === expanded) || null;

  // gallery state
  let galleryIndex = 0;

  function openProject(id) {
    expanded = id;
    galleryIndex = 0;
    window.scrollTo({ top: 0, behavior: 'smooth' });
  }

  function closeProject() {
    expanded = null;
    galleryIndex = 0;
  }

  function showImage(i) {
    galleryIndex = i;
  }

  // image navigation (wrap-around)
  function nextImage() {
    if (!selected) return;
    const len = (selected.images?.length || 1);
    galleryIndex = (galleryIndex + 1) % len;
  }

  function prevImage() {
    if (!selected) return;
    const len = (selected.images?.length || 1);
    galleryIndex = (galleryIndex - 1 + len) % len;
  }

  // keyboard support for gallery and escape to close
  function onKeydown(e) {
    if (!selected) return;
    if (e.key === 'Escape') closeProject();
    if (e.key === 'ArrowRight') nextImage();
    if (e.key === 'ArrowLeft') prevImage();
  }

  $: {
    if (selected) {
      window.addEventListener('keydown', onKeydown);
    } else {
      window.removeEventListener('keydown', onKeydown);
    }
  }
</script>

<main class="container">
  <!-- Header (keeps your original fonts and nav layout) -->
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
    <p class="subtitle">Click a project to open a detailed view with images, links, and notes.</p>
  </header>

  <section class="projects">
    {#if !selected}
      <h2 class="section-title">List of Projects</h2>
      <div class="project-list" role="list">
        {#each projects as project}
          <article class="project-row" role="listitem" on:click={() => openProject(project.id)}>
            {#if project.thumb}
              <img class="thumb" src={project.thumb} alt={`${project.title} thumbnail`} loading="lazy" />
            {:else}
              <div class="thumb placeholder" aria-hidden="true"></div>
            {/if}
            <div class="meta">
              <h3 class="proj-title">{project.title}</h3>
              <p class="preview">{project.preview}</p>
              <div class="row-meta">
                <span class="role">{project.role}</span>
                <span class="date">{project.date}</span>
              </div>
            </div>
          </article>
        {/each}
      </div>
    {:else}
      <!-- Focused project page -->
      <section class="project-focus" aria-live="polite">
        <div class="focus-controls">
          <button class="back-btn" on:click={closeProject}>← Back</button>

          {#if selected.images && selected.images.length > 1}
            <div class="nav-controls">
              <button class="nav-btn" on:click={prevImage} aria-label="Previous image">◀</button>
              <button class="nav-btn" on:click={nextImage} aria-label="Next image">▶</button>
            </div>
          {/if}
        </div>

        <header class="focus-header">
          <div class="focus-left">
            <h2 class="focus-title">{selected.title}</h2>

            <div class="meta-row">
              <span class="role">{selected.role}</span>
              <span class="date">{selected.date}</span>
              <div class="tags">
                {#each selected.tags ?? [] as t}
                  <span class="tag">{t}</span>
                {/each}
              </div>
            </div>

            <p class="lead">{selected.preview}</p>

            <div class="links">
              {#each selected.links ?? [] as link}
                <a class="link" href={link.href} target={link.external ? "_blank" : "_self"} rel={link.external ? "noopener noreferrer" : undefined}>
                  {link.label}
                </a>
              {/each}
            </div>

            <div class="tech">
              <strong>Tech:</strong> {selected.tech?.join(', ')}
            </div>
          </div>

          <!-- Gallery -->
          <div class="gallery" aria-hidden={selected.images?.length ? "false" : "true"}>
            {#if selected.images && selected.images.length > 0}
              <div class="main-image-wrap">
                <img class="main-image" src={selected.images[galleryIndex]} alt={`${selected.title} image ${galleryIndex + 1}`} loading="lazy" />
              </div>

              <div class="thumb-row">
                {#each selected.images as img, i}
                  <button class="thumb-btn {i === galleryIndex ? 'active' : ''}" on:click={() => showImage(i)} aria-label={"Show image " + (i+1)}>
                    <img src={img} alt="" loading="lazy" />
                  </button>
                {/each}
              </div>
            {:else}
              <div class="no-image">No images for this project</div>
            {/if}
          </div>
        </header>

        <article class="focus-body">
          {#each selected.content as paragraph}
            <p>{paragraph}</p>
          {/each}

          {#if selected.bullets && selected.bullets.length}
            <ul>
              {#each selected.bullets as b}
                <li>{b}</li>
              {/each}
            </ul>
          {/if}

          {#if selected.codeUrl}
            <CodePanel codeUrl={selected.codeUrl} />
          {/if}

          {#if selected.embed}
            <div class="embed" innerHTML={selected.embed}></div>
          {/if}
        </article>
      </section>
    {/if}
  </section>
</main>

<style>
  /* --- NAV & HEADER: keep your original layout and fonts unchanged --- */
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

  /* --- Projects list & focused view (inherits your fonts) --- */
  .projects { margin-top: 1.5rem; }

  .section-title { margin: 0 0 0.75rem 0; color: #0b2545; }

  .project-list {
    display: flex;
    flex-direction: column;
    gap: 0.9rem;
    max-height: 60vh;
    overflow-y: auto;
    padding-right: 0.5rem;
  }

  .project-row {
    display: flex;
    gap: 0.9rem;
    align-items: center;
    padding: 0.6rem;
    border-radius: 8px;
    background: #fafafa;
    border: 1px solid #e6e6e6;
    cursor: pointer;
    transition: transform 0.12s ease, box-shadow 0.12s ease;
  }
  .project-row:hover { transform: translateY(-3px); box-shadow: 0 6px 18px rgba(0,0,0,0.06); }

  .thumb { width: 72px; height: 72px; object-fit: cover; border-radius: 6px; flex: 0 0 72px; box-shadow: 0 2px 6px rgba(0,0,0,0.08); }
  .thumb.placeholder { background: linear-gradient(135deg,#eee,#f7f7f7); }

  .meta { display:flex; flex-direction:column; min-width:0; }
  .proj-title {
    margin:0;
    font-size:1.05rem;
    color:#0b2545;
    white-space:nowrap;
    overflow:hidden;
    text-overflow:ellipsis;
  }

  .preview {
    margin:0.25rem 0 0;
    color:#334155;
    font-size:0.9rem;
    display:-webkit-box;
    -webkit-line-clamp:2;
    -webkit-box-orient:vertical;
    overflow:hidden;
  }

  .row-meta { margin-top:0.4rem; display:flex; gap:0.6rem; align-items:center; color:#567; font-size:0.85rem; }
  .role { font-weight:600; color:#234; }
  .date { color:#567; }

  /* Focused project */
  .project-focus { margin-top:1rem; padding:1rem; background:#fff; border-radius:8px; border:1px solid #e6e6e6; }
  .focus-controls { display:flex; justify-content:space-between; align-items:center; gap:1rem; margin-bottom:0.75rem; }
  .back-btn { background:none; border:2px solid #567; color:#567; padding:0.4rem 0.8rem; border-radius:6px; cursor:pointer; font-weight:600; }
  .nav-controls { display:flex; gap:0.5rem; }
  .nav-btn { background:#f5f5f5; border:1px solid #ddd; padding:0.3rem 0.6rem; border-radius:6px; cursor:pointer; }

  .focus-header { display:flex; gap:1.25rem; align-items:flex-start; flex-wrap:wrap; }
  .focus-left { flex:1 1 360px; min-width:260px; }
  .focus-title { margin:0 0 0.25rem 0; color:#0b2545; font-size:1.6rem; }
  .meta-row { display:flex; gap:0.6rem; align-items:center; margin-bottom:0.5rem; flex-wrap:wrap; }
  .tags { display:flex; gap:0.4rem; }
  .tag { background:#f0f6ff; color:#0b2545; padding:0.15rem 0.5rem; border-radius:6px; font-size:0.8rem; }

  .lead { margin:0 0 0.75rem 0; color:#334155; }

  .links { display:flex; gap:0.6rem; flex-wrap:wrap; margin-bottom:0.5rem; }
  .link { color:#0b2545; text-decoration:underline; font-weight:600; }

  .tech { color:#334155; font-size:0.95rem; margin-top:0.5rem; }

  /* Gallery */
  .gallery { width:320px; max-width:40%; min-width:220px; display:flex; flex-direction:column; gap:0.5rem; }
  .main-image-wrap { background:#f7f7f7; border-radius:8px; overflow:hidden; display:flex; align-items:center; justify-content:center; height:200px; }
  .main-image { width:100%; height:100%; object-fit:cover; display:block; }
  .thumb-row { display:flex; gap:0.4rem; margin-top:0.4rem; overflow-x:auto; }
  .thumb-btn { border:1px solid #eee; padding:0; background:#fff; border-radius:6px; cursor:pointer; }
  .thumb-btn img { width:64px; height:48px; object-fit:cover; display:block; border-radius:6px; }
  .thumb-btn.active { outline:3px solid rgba(11,37,69,0.12); }

  .no-image { color:#567; padding:1rem; border-radius:6px; background:#fafafa; }

  .focus-body { margin-top:1rem; color:#444; line-height:1.6; }
  .focus-body ul { margin-left:1.2rem; }

  /* responsive */
  @media (max-width: 900px) {
    .focus-header { flex-direction:column; }
    .gallery { width:100%; max-width:100%; min-width:0; }
    .main-image-wrap { height:220px; }
  }
</style>
