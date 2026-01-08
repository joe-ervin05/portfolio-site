<script lang="ts">
  import { fly, fade } from "svelte/transition";
  import { Button } from "$lib/components/ui/button";
  import { Card } from "$lib/components/ui/card";
  import { Mail, Github, Linkedin, MapPin } from "@lucide/svelte";

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

<section id="contact" class="py-24 px-6 bg-muted/30" bind:this={sectionRef}>
  <div class="max-w-2xl mx-auto">
    {#if sectionVisible}
      <Card class="p-6 md:p-8">
        <div class="flex flex-col md:flex-row items-center gap-6 md:gap-8">
          <div
            in:fly={{ x: -30, duration: 600, delay: 50 }}
            class="shrink-0 p-4 rounded-none bg-muted border border-foreground/10"
          >
            <Mail class="h-8 w-8 text-muted-foreground" />
          </div>

          <div class="flex flex-col gap-2 text-center md:text-left">
            <div in:fly={{ y: -20, duration: 600, delay: 100 }}>
              <p
                class="text-muted-foreground font-medium tracking-wide uppercase text-xs mb-1"
              >
                Get in Touch
              </p>
              <h2 class="text-2xl md:text-3xl font-bold tracking-tight">
                Let's Talk
              </h2>
            </div>

            <p
              in:fly={{ y: -20, duration: 600, delay: 200 }}
              class="text-base text-muted-foreground max-w-md leading-relaxed"
            >
              I'm actively looking for internship opportunities. Feel free to
              reach out!
            </p>
          </div>
        </div>

        <div
          in:fly={{ y: -20, duration: 600, delay: 300 }}
          class="flex flex-col md:flex-row items-center justify-center gap-4 md:gap-6 mt-6 pt-6 border-t"
        >
          <div class="flex items-center gap-3">
            <Button
              variant="default"
              size="lg"
              href="mailto:joe_ervin10@outlook.com"
            >
              <Mail class="mr-2 h-4 w-4" />
              Email Me
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
              class="p-2 rounded-none border-2 border-foreground/20 text-muted-foreground hover:text-foreground hover:border-foreground/40 shadow-[2px_2px_0px_0px] shadow-foreground/10 hover:shadow-[1px_1px_0px_0px] hover:translate-x-[1px] hover:translate-y-[1px] transition-all"
              aria-label="GitHub"
            >
              <Github class="h-5 w-5" />
            </a>
            <a
              href="https://linkedin.com/in/joeervin05"
              target="_blank"
              rel="noopener noreferrer"
              class="p-2 rounded-none border-2 border-foreground/20 text-muted-foreground hover:text-foreground hover:border-foreground/40 shadow-[2px_2px_0px_0px] shadow-foreground/10 hover:shadow-[1px_1px_0px_0px] hover:translate-x-[1px] hover:translate-y-[1px] transition-all"
              aria-label="LinkedIn"
            >
              <Linkedin class="h-5 w-5" />
            </a>
            <a
              href="mailto:joe_ervin10@outlook.com"
              class="p-2 rounded-none border-2 border-foreground/20 text-muted-foreground hover:text-foreground hover:border-foreground/40 shadow-[2px_2px_0px_0px] shadow-foreground/10 hover:shadow-[1px_1px_0px_0px] hover:translate-x-[1px] hover:translate-y-[1px] transition-all"
              aria-label="Email"
            >
              <Mail class="h-5 w-5" />
            </a>
          </div>
        </div>
      </Card>

      <p
        in:fade={{ duration: 500, delay: 600 }}
        class="text-center text-sm text-muted-foreground mt-6 flex items-center justify-center gap-2"
      >
        <MapPin class="h-4 w-4" />
        Open to remote and on-site opportunities
      </p>
    {/if}
  </div>
</section>
