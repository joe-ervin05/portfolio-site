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
      title: "Task Management App",
      description:
        "A full-stack task management application with real-time updates, user authentication, and collaborative features.",
      technologies: ["React", "Node.js", "PostgreSQL", "Socket.io"],
      githubUrl: "https://github.com",
      liveUrl: "https://example.com",
    },
    {
      title: "E-commerce Platform",
      description:
        "A modern e-commerce solution with product catalog, shopping cart, payment integration, and admin dashboard.",
      technologies: ["Next.js", "TypeScript", "Prisma", "Stripe"],
      githubUrl: "https://github.com",
    },
    {
      title: "Weather Dashboard",
      description:
        "A responsive weather application featuring location-based forecasts, interactive maps, and data visualization.",
      technologies: ["Vue.js", "D3.js", "OpenWeather API"],
      githubUrl: "https://github.com",
      liveUrl: "https://example.com",
    },
    {
      title: "CLI Productivity Tool",
      description:
        "A command-line tool for developers to automate repetitive tasks and improve workflow efficiency.",
      technologies: ["Rust", "CLI", "Async Runtime"],
      githubUrl: "https://github.com",
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
              class="h-full flex flex-col hover:ring-4 hover:ring-muted transition-all duration-300 group"
            >
              <Card.Header>
                <div class="flex items-start justify-between">
                  <div class="p-2 rounded-lg bg-muted ring-2 ring-border mb-2">
                    <Folder class="h-6 w-6 text-primary" />
                  </div>
                  <div class="flex gap-3">
                    {#if project.githubUrl}
                      <a
                        href={project.githubUrl}
                        target="_blank"
                        rel="noopener noreferrer"
                        class="p-2 rounded-lg text-muted-foreground hover:text-foreground hover:bg-muted transition-all"
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
                        class="p-2 rounded-lg text-muted-foreground hover:text-foreground hover:bg-muted transition-all"
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
                    <Badge variant="secondary" class="text-xs font-medium rounded-md">
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
