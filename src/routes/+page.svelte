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

<main class="min-h-screen">
  <Hero />
  <Projects />
  <Contact />

  <footer class="py-8 px-6 bg-muted/30">
    <div class="max-w-6xl mx-auto">
      <div
        class="flex flex-col md:flex-row items-center justify-between gap-4 py-4 px-6 rounded-lg bg-card border ring-1 ring-border"
      >
        <p class="text-sm text-muted-foreground">
          &copy; {new Date().getFullYear()} Joe Ervin
        </p>
        <p class="text-sm text-muted-foreground">
          Built with SvelteKit & Tailwind
        </p>
      </div>
    </div>
  </footer>
</main>
