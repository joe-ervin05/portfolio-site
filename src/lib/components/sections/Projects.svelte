<script lang="ts">
  import { fly } from "svelte/transition";
  import * as Card from "$lib/components/ui/card";
  import { Badge } from "$lib/components/ui/badge";
  import { ExternalLink, Github, Folder } from "@lucide/svelte";

  interface Project {
    title: string;
    description: string;
    technologies: string[];
    githubUrl?: string;
    liveUrl?: string;
  }

  const projects: Project[] = [
    {
      title: "Atomicbase",
      description:
        "The backend for effortless multi-tenant architecture. It's an API built on top of LibSQL and Turso and will eventually be a complete backend solution with authentication, file storage, a dashboard, and client SDKs.",
      technologies: ["Golang", "SQLite", "Turso", "TypeScript"],
      githubUrl: "https://github.com/joe-ervin05/atomicbase-2",
    },
    {
      title: "Pagerush Engine",
      description:
        "A work-in-progress engine for building web pages in a way that maps well to site builders.",
      technologies: [
        "Bun",
        "TypeScript",
        "ESBuild",
        "PostCSS",
        "Liquid.JS",
        "Tailwind CSS",
      ],
      githubUrl: "https://github.com/joe-ervin05/pagerush-engine",
    },
    {
      title: "Portfolio Website",
      description:
        "The site you're on right now! A neo-retro portfolio featuring an animated space-themed background with twinkling stars, shooting stars, and smooth transitions.",
      technologies: ["SvelteKit", "TypeScript", "Tailwind CSS"],
      githubUrl: "https://github.com/joe-ervin05/portfolio-site",
    },
    {
      title: "Word Link",
      description:
        "A terminal-based program that finds the shortest path between two 5 letter words in a dictionary.",
      technologies: ["Golang", "Graph data structures", "DFS algorithm"],
    },
  ];

  let sectionVisible = $state(false);
  let sectionRef: HTMLElement | undefined = $state(undefined);

  $effect(() => {
    if (!sectionRef) return;

    const observer = new IntersectionObserver(
      (entries) => {
        entries.forEach((entry) => {
          if (entry.isIntersecting) {
            sectionVisible = true;
          }
        });
      },
      { threshold: 0.1 }
    );

    observer.observe(sectionRef);

    return () => observer.disconnect();
  });
</script>

<section id="projects" class="py-24 px-6" bind:this={sectionRef}>
  <div class="max-w-6xl mx-auto">
    {#if sectionVisible}
      <div class="text-center mb-16">
        <p
          in:fly={{ y: 20, duration: 500 }}
          class="text-muted-foreground font-medium tracking-wide uppercase text-xs mb-2"
        >
          Portfolio
        </p>
        <h2
          in:fly={{ y: 20, duration: 500, delay: 50 }}
          class="text-3xl md:text-4xl font-bold tracking-tight mb-4"
        >
          Featured Projects
        </h2>
        <p
          in:fly={{ y: 20, duration: 500, delay: 100 }}
          class="text-muted-foreground max-w-lg mx-auto"
        >
          A selection of projects that showcase my skills in building complex
          applications.
        </p>
      </div>

      <div class="grid grid-cols-1 md:grid-cols-2 gap-6">
        {#each projects as project, i}
          <div in:fly={{ y: 30, duration: 500, delay: 150 + i * 100 }}>
            <Card.Root
              class="h-full flex flex-col hover:translate-x-[-2px] hover:translate-y-[-2px] hover:shadow-[8px_8px_0px_0px] hover:shadow-foreground/10 transition-all duration-300 group"
            >
              <Card.Header>
                <div class="flex items-start justify-between">
                  <Folder class="h-6 w-6 text-muted-foreground mb-2" />
                  <div class="flex gap-3">
                    {#if project.githubUrl}
                      <a
                        href={project.githubUrl}
                        target="_blank"
                        rel="noopener noreferrer"
                        class="p-2 rounded-none border-2 border-foreground/20 text-muted-foreground hover:text-foreground hover:border-foreground/40 shadow-[2px_2px_0px_0px] shadow-foreground/10 hover:shadow-[1px_1px_0px_0px] hover:translate-x-[1px] hover:translate-y-[1px] transition-all"
                        aria-label="View source on GitHub"
                      >
                        <Github class="h-5 w-5" />
                      </a>
                    {/if}
                    {#if project.liveUrl}
                      <a
                        href={project.liveUrl}
                        target="_blank"
                        rel="noopener noreferrer"
                        class="p-2 rounded-none border-2 border-foreground/20 text-muted-foreground hover:text-foreground hover:border-foreground/40 shadow-[2px_2px_0px_0px] shadow-foreground/10 hover:shadow-[1px_1px_0px_0px] hover:translate-x-[1px] hover:translate-y-[1px] transition-all"
                        aria-label="View live demo"
                      >
                        <ExternalLink class="h-5 w-5" />
                      </a>
                    {/if}
                  </div>
                </div>
                <Card.Title class="group-hover:text-primary transition-colors">
                  {project.title}
                </Card.Title>
              </Card.Header>
              <Card.Content class="flex-1">
                <p class="text-muted-foreground text-sm leading-relaxed">
                  {project.description}
                </p>
              </Card.Content>
              <Card.Footer>
                <div class="flex flex-wrap gap-2">
                  {#each project.technologies as tech}
                    <Badge variant="secondary">
                      {tech}
                    </Badge>
                  {/each}
                </div>
              </Card.Footer>
            </Card.Root>
          </div>
        {/each}
      </div>
    {/if}
  </div>
</section>
