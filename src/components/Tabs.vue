<template>
  <!-- Tab list -->
  <div class="px-4 sm:px-0">
    <div class="sm:hidden">
      <label for="question-tabs" class="sr-only">Select a tab</label>
      <select id="question-tabs"
              class="block w-full rounded border-zinc-300 text-base font-medium text-zinc-900 shadow-sm focus:border-emerald-500 focus:ring-emerald-500"
              v-model="current_tab">
        <option v-for="tab in tabs" :key="tab.name" :selected="tab.current">{{ tab.name }}</option>
      </select>
    </div>

    <div class="hidden sm:block">
      <nav class="relative z-0 rounded shadow-lg flex divide-x divide-zinc-600" aria-label="Tabs">
        <a v-for="(tab, tabIdx) in tabs" :key="tab.name" :href="tab.href"
           :aria-current="tab.current ? 'page' : undefined"
           :class="[tab.current ? 'text-zinc-300' : 'text-zinc-100 brand-transition hover:text-zinc-900 hover:bg-zinc-300', tabIdx === 0 ? 'rounded-l' : '', tabIdx === tabs.length - 1 ? 'rounded-r' : '', 'group relative min-w-0 flex-1 overflow-hidden bg-zinc-900 py-4 px-6 text-sm font-medium text-center focus:z-10']">
          <span>{{ tab.name }}</span>
          <span aria-hidden="true"
                :class="[tab.current ? 'bg-emerald-500' : 'bg-transparent', 'absolute inset-x-0 bottom-0 h-0.5']"/>
        </a>
      </nav>
    </div>
  </div>

  <!-- Tab content-->
  <div class="mt-4">
    <h1 class="sr-only">
      {{ current_tab }}
    </h1>
    <ul role="list" class="space-y-4">
      <li v-for="content in contents" :key="content.id"
          class="bg-zinc-900 px-4 py-6 shadow sm:p-6 sm:rounded">
        <article :aria-labelledby="'content-title-' + content.id">
          <div>
            <div class="flex space-x-3">
              <div class="flex-shrink-0">
                <img class="h-10 w-10 rounded-full" :src="content.author.imageUrl" alt=""/>
              </div>
              <div class="min-w-0 flex-1">
                <p class="text-sm font-medium text-zinc-100">
                  <a :href="content.author.href" class="hover:underline">{{ content.author.name }}</a>
                </p>
                <p class="text-sm text-zinc-500">
                  <a :href="content.href" class="hover:underline">
                    <time :datetime="content.datetime">{{ content.date }}</time>
                  </a>
                </p>
              </div>
              <div class="flex-shrink-0 self-center flex">
                <Menu as="div" class="relative inline-block text-left">
                  <div>
                    <MenuButton
                        class="-m-2 p-2 rounded-full flex items-center text-zinc-300 hover:text-zinc-100">
                      <span class="sr-only">Open options</span>
                      <DotsVerticalIcon class="h-5 w-5" aria-hidden="true"/>
                    </MenuButton>
                  </div>

                  <transition enter-active-class="transition ease-out duration-100"
                              enter-from-class="transform opacity-0 scale-95"
                              enter-to-class="transform opacity-100 scale-100"
                              leave-active-class="transition ease-in duration-75"
                              leave-from-class="transform opacity-100 scale-100"
                              leave-to-class="transform opacity-0 scale-95">
                    <MenuItems
                        class="origin-top-right absolute right-0 mt-2 w-56 rounded shadow-lg bg-white ring-1 ring-black ring-opacity-5 focus:outline-none">
                      <div class="py-1">
                        <MenuItem v-slot="{ active }">
                          <a href="#"
                             :class="[active ? 'bg-zinc-100 text-zinc-900' : 'text-zinc-700', 'flex px-4 py-2 text-sm']">
                            <StarIcon class="mr-3 h-5 w-5 text-zinc-400" aria-hidden="true"/>
                            <span>Add to favorites</span>
                          </a>
                        </MenuItem>
                        <MenuItem v-slot="{ active }">
                          <a href="#"
                             :class="[active ? 'bg-zinc-100 text-zinc-900' : 'text-zinc-700', 'flex px-4 py-2 text-sm']">
                            <CodeIcon class="mr-3 h-5 w-5 text-zinc-400" aria-hidden="true"/>
                            <span>Embed</span>
                          </a>
                        </MenuItem>
                        <MenuItem v-slot="{ active }">
                          <a href="#"
                             :class="[active ? 'bg-zinc-100 text-zinc-900' : 'text-zinc-700', 'flex px-4 py-2 text-sm']">
                            <FlagIcon class="mr-3 h-5 w-5 text-zinc-400" aria-hidden="true"/>
                            <span>Report content</span>
                          </a>
                        </MenuItem>
                      </div>
                    </MenuItems>
                  </transition>
                </Menu>
              </div>
            </div>

            <h2 :id="'content-title-' + content.id" class="mt-4 text-base font-medium text-zinc-100">
              {{ content.title }}
            </h2>
          </div>
          <div class="mt-2 text-sm text-zinc-300 space-y-4" v-html="content.body"/>
          <div class="mt-6 flex justify-between space-x-8">
            <div class="flex space-x-6">
              <span class="inline-flex items-center text-sm">
                <button type="button" class="inline-flex space-x-2 text-zinc-400 hover:text-zinc-200">
                  <ThumbUpIcon class="h-5 w-5" aria-hidden="true"/>
                  <span class="font-medium text-zinc-100">{{ content.likes }}</span>
                  <span class="sr-only">likes</span>
                </button>
              </span>
              <span class="inline-flex items-center text-sm">
                <button type="button" class="inline-flex space-x-2 text-zinc-400 hover:text-zinc-200">
                  <ChatAltIcon class="h-5 w-5" aria-hidden="true"/>
                  <span class="font-medium text-zinc-100">{{ content.replies }}</span>
                  <span class="sr-only">replies</span>
                </button>
              </span>
              <span class="inline-flex items-center text-sm">
                <button type="button" class="inline-flex space-x-2 text-zinc-400 hover:text-zinc-200">
                  <EyeIcon class="h-5 w-5" aria-hidden="true"/>
                  <span class="font-medium text-zinc-100">{{ content.views }}</span>
                  <span class="sr-only">views</span>
                </button>
              </span>
            </div>
            <div class="flex text-sm">
              <span class="inline-flex items-center text-sm">
                <button type="button" class="inline-flex space-x-2 text-zinc-400 hover:text-zinc-200">
                  <ShareIcon class="h-5 w-5" aria-hidden="true"/>
                  <span class="sr-only">Share</span>
                </button>
              </span>
            </div>
          </div>
        </article>
      </li>
    </ul>
  </div>
</template>

<script setup>
import {Menu, MenuButton, MenuItem, MenuItems} from '@headlessui/vue'
import {
  DotsVerticalIcon,
  StarIcon,
  CodeIcon,
  FlagIcon,
  ThumbUpIcon,
  ChatAltIcon,
  EyeIcon,
  ShareIcon
} from '@heroicons/vue/solid'
import {ref} from "vue";

const props = defineProps({
  tabs: Array,
  contents: Array,
});

let current_tab = ref(getCurrentTab());

function getCurrentTab() {
  const tab = Array.from(props.tabs).find((tab) => {
    return tab.current === true
  });
  return tab.name;
}
</script>

<style scoped>

</style>