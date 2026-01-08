<script lang="ts">
  import { fly, fade } from "svelte/transition";
  import { Button } from "$lib/components/ui/button";
  import { Card } from "$lib/components/ui/card";
  import { ArrowDown, Github, Linkedin, Mail } from "@lucide/svelte";
  import CylinderGrid from "$lib/components/CylinderGrid.svelte";

  let visible = $state(false);

  $effect(() => {
    visible = true;
  });
</script>

<section
  class="min-h-screen flex flex-col justify-center items-center px-6 py-20 relative overflow-hidden"
>
  <CylinderGrid />

  {#if visible}
    <div
      class="max-w-4xl w-full flex flex-col items-center gap-5 relative z-10"
    >
      <Card
        class="flex flex-col md:flex-row items-center gap-6 md:gap-8 p-6 md:p-8"
      >
        <div in:fly={{ x: -30, duration: 600, delay: 50 }} class="shrink-0">
          <img
            src="/profile.jpg"
            alt="Joe Ervin"
            class="w-24 h-24 md:w-28 md:h-28 rounded-lg object-cover ring-4 ring-muted"
          />
        </div>

        <div class="flex flex-col gap-2 text-center md:text-left">
          <div in:fly={{ y: -20, duration: 600, delay: 100 }}>
            <p
              class="text-muted-foreground font-medium tracking-wide uppercase text-xs mb-1"
            >
              Software Engineer
            </p>
            <h1 class="text-3xl md:text-4xl font-bold tracking-tight">
              Hi, I'm <span class="text-primary">Joe Ervin</span>
            </h1>
          </div>

          <p
            in:fly={{ y: -20, duration: 600, delay: 200 }}
            class="text-base text-muted-foreground max-w-md leading-relaxed"
          >
            A computer science student at UCF seeking software engineering
            internship opportunities.
          </p>
        </div>
      </Card>

      <div
        in:fly={{ y: -20, duration: 600, delay: 300 }}
        class="flex flex-col md:flex-row items-center justify-center gap-4 md:gap-6"
      >
        <div class="flex items-center gap-3">
          <Button variant="default" size="lg" href="#contact">
            Get in Touch
            <Mail class="ml-2 h-4 w-4" />
          </Button>
          <Button variant="outline" size="lg" href="#projects">
            View Projects
            <ArrowDown class="ml-2 h-4 w-4" />
          </Button>
        </div>

        <div class="hidden md:block w-px h-8 bg-border"></div>

        <div
          in:fade={{ duration: 600, delay: 500 }}
          class="flex items-center gap-4"
        >
          <a
            href="https://github.com/joe-ervin05"
            target="_blank"
            rel="noopener noreferrer"
            class="text-muted-foreground hover:text-foreground transition-colors duration-200"
            aria-label="GitHub"
          >
            <Github class="h-5 w-5" />
          </a>
          <a
            href="https://linkedin.com/in/joeervin05"
            target="_blank"
            rel="noopener noreferrer"
            class="text-muted-foreground hover:text-foreground transition-colors duration-200"
            aria-label="LinkedIn"
          >
            <Linkedin class="h-5 w-5" />
          </a>
          <a
            href="mailto:joe_ervin10@outlook.com"
            class="text-muted-foreground hover:text-foreground transition-colors duration-200"
            aria-label="Email"
          >
            <Mail class="h-5 w-5" />
          </a>
        </div>
      </div>
    </div>
  {/if}

  <a href="#projects" class="absolute bottom-8 left-1/2 -translate-x-1/2">
    {#if visible}
      <div in:fade={{ duration: 600, delay: 700 }} class="animate-bounce">
        <ArrowDown class="h-8 w-8 text-muted-foreground" />
      </div>
    {/if}
  </a>
</section>
