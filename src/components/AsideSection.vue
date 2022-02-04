<template>
  <section :aria-labelledby="heading + '-heading'">
    <div class="bg-zinc-900 rounded shadow">
      <div class="p-6">
        <h2 :id="heading + '-heading'" class="text-base font-medium text-zinc-100">
          {{ title }}
        </h2>
        <div class="mt-6 flow-root">
          <slot></slot>
        </div>
        <div class="mt-6">
          <a href="#"
             class="w-full block text-center px-4 py-2 border border-zinc-600 shadow-sm text-sm font-medium rounded text-zinc-200 bg-zinc-800 brand-transition hover:text-zinc-900 hover:bg-zinc-300">
            View all
          </a>
        </div>
      </div>
    </div>
  </section>
</template>

<script setup>

const props = defineProps({
  title: String,
});

const heading = props.title.toString().replace(/\s/g, '-').toLowerCase();
</script>

<style scoped>

</style>