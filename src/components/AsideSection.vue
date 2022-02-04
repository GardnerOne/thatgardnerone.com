<template>
  <section :aria-labelledby="heading + '-heading'">
    <div class="bg-white rounded-lg shadow">
      <div class="p-6">
        <h2 :id="heading + '-heading'" class="text-base font-medium text-gray-900">
          {{ title }}
        </h2>
        <div class="mt-6 flow-root">
          <slot></slot>
        </div>
        <div class="mt-6">
          <a href="#"
             class="w-full block text-center px-4 py-2 border border-gray-300 shadow-sm text-sm font-medium rounded-md text-gray-700 bg-white hover:bg-gray-50">
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