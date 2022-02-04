<template>
  <div class="hidden lg:block lg:col-span-3 xl:col-span-2">
    <nav aria-label="Sidebar" class="sticky top-4 divide-y divide-emerald-900">
      <div class="pb-8 space-y-1">
        <a v-for="item in navigation"
           :key="item.name"
           :href="item.href"
           :class="[item.current ? 'text-zinc-400 bg-zinc-900' : 'text-zinc-300 brand-transition hover:text-zinc-900 hover:bg-zinc-300', 'group flex items-center px-3 py-2 text-sm font-medium rounded']"
           :aria-current="item.current ? 'page' : undefined">
          <component :is="item.icon" :class="[item.current ? 'text-zinc-300' : 'text-zinc-400 brand-transition group-hover:text-zinc-900', 'flex-shrink-0 -ml-1 mr-3 h-6 w-6']" aria-hidden="true" />
          <span class="truncate">
              {{ item.name }}
            </span>
        </a>
      </div>
      <div class="pt-10">
        <p class="px-3 text-xs font-semibold text-zinc-100 uppercase tracking-wider" id="projects-headline">
          My Projects
        </p>
        <div class="mt-3 space-y-2" aria-labelledby="projects-headline">
          <a v-for="project in projects"
             :key="project.name"
             :href="project.href"
             class="group flex items-center px-3 py-2 text-sm font-medium text-zinc-300 rounded brand-transition hover:text-zinc-900 hover:bg-zinc-300">
            <span class="truncate">
              {{ project.name }}
            </span>
          </a>
        </div>
      </div>
    </nav>
  </div>
</template>

<script setup>
const projects = [
  { name: 'Movies', href: '#' },
  { name: 'Food', href: '#' },
  { name: 'Sports', href: '#' },
  { name: 'Animals', href: '#' },
  { name: 'Science', href: '#' },
  { name: 'Dinosaurs', href: '#' },
  { name: 'Talents', href: '#' },
  { name: 'Gaming', href: '#' },
]

defineProps({
  navigation: Array,
});

</script>

<style scoped>

</style>