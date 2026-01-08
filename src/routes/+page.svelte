<script lang="ts">
  import Hero from "$lib/components/sections/Hero.svelte";
  import Projects from "$lib/components/sections/Projects.svelte";
  import Contact from "$lib/components/sections/Contact.svelte";
</script>

<svelte:head>
  <title>Joe Ervin | Software Engineer</title>
  <meta
    name="description"
    content="Software Engineer seeking internship opportunities. Explore my projects and get in touch."
  />
</svelte:head>

<main class="min-h-screen relative z-10">
  <Hero />
  <Projects />
  <Contact />

  <footer class="py-8 px-6 border-t-2 border-foreground/10">
    <div class="max-w-6xl mx-auto flex flex-col md:flex-row items-center justify-between gap-4">
      <p class="text-xs text-muted-foreground uppercase tracking-wide">
        &copy; {new Date().getFullYear()} Joe Ervin
      </p>
      <p class="text-xs text-muted-foreground uppercase tracking-wide">
        Built with SvelteKit & Tailwind
      </p>
    </div>
  </footer>
</main>
