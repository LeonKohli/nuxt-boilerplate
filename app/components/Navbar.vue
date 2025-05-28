<template>
  <header
    role="banner"
    class="sticky top-0 z-20 border-b backdrop-blur supports-backdrop-blur:bg-background/60 px-4 md:px-8"
  >
    <div class="max-w-8xl mx-auto h-16 flex items-center justify-between">
      <NuxtLink to="/" class="flex items-center space-x-3 group" aria-label="Home">
        <Icon name="lucide:zap" class="h-8 w-8 text-primary transition-opacity group-hover:opacity-80" />
        <div>
          <span class="font-semibold text-lg tracking-tight transition-opacity group-hover:opacity-80">Nuxt Shadcn Boilerplate</span>
          <p class="text-xs text-muted-foreground transition-opacity group-hover:opacity-80 hidden md:block">Modern development stack</p>
        </div>
      </NuxtLink>

      <div class="flex items-center">
        <ClientOnly> 
          <ColorModeToggle />
          <template #fallback>
            <div class="w-10 h-10"></div>
          </template>
        </ClientOnly>
        <Button variant="ghost" size="icon" as="a" href="https://github.com" target="_blank" rel="noopener" class="ml-1" aria-label="GitHub Repository">
          <Icon name="lucide:github" class="w-5 h-5" />
        </Button>
      </div>
    </div>
  </header>
</template> 