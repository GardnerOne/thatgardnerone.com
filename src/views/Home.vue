<template>
  <div class="min-h-full bg-black">
    <Navigation :navigation="navigation"/>

    <div class="py-10">
      <div class="max-w-3xl mx-auto sm:px-6 lg:max-w-none lg:px-8 lg:grid lg:grid-cols-12 lg:gap-8">
        <Sidebar :navigation="navigation"/>
        <main class="lg:col-span-9 xl:col-span-7">
          <Tabs :tabs="tabs" :contents="questions" />
        </main>
        <Aside>
            <AsideSection title="Who to follow">
              <ul role="list" class="-my-4 divide-y divide-zinc-600">
                <li v-for="user in whoToFollow" :key="user.handle" class="flex items-center py-4 space-x-3">
                  <div class="flex-shrink-0">
                    <img class="h-8 w-8 rounded-full" :src="user.imageUrl" alt=""/>
                  </div>
                  <div class="min-w-0 flex-1">
                    <p class="text-sm font-medium text-zinc-100">
                      <a :href="user.href">{{ user.name }}</a>
                    </p>
                    <p class="text-sm text-zinc-500">
                      <a :href="user.href">{{ '@' + user.handle }}</a>
                    </p>
                  </div>
                  <div class="flex-shrink-0">
                    <button type="button"
                            class="inline-flex items-center px-3 py-0.5 rounded-full bg-zinc-300 text-sm font-medium text-zinc-900 hover:bg-emerald-500">
                      <PlusSmIcon class="-ml-1 mr-0.5 h-5 w-5 text-zinc-900" aria-hidden="true"/>
                      <span>
                        Follow
                      </span>
                    </button>
                  </div>
                </li>
              </ul>
            </AsideSection>
            <AsideSection title="Trending">
              <ul role="list" class="-my-4 divide-y divide-zinc-600">
                <li v-for="post in trendingPosts" :key="post.id" class="flex py-4 space-x-3">
                  <div class="flex-shrink-0">
                    <img class="h-8 w-8 rounded-full" :src="post.user.imageUrl" :alt="post.user.name"/>
                  </div>
                  <div class="min-w-0 flex-1">
                    <p class="text-sm text-zinc-200">{{ post.body }}</p>
                    <div class="mt-2 flex">
                      <span class="inline-flex items-center text-sm">
                        <button type="button" class="inline-flex space-x-2 text-zinc-400 hover:text-zinc-200">
                          <ChatAltIcon class="h-5 w-5" aria-hidden="true"/>
                          <span class="font-medium text-zinc-100">{{ post.comments }}</span>
                        </button>
                      </span>
                    </div>
                  </div>
                </li>
              </ul>
            </AsideSection>
            <AsideSection title="Latest">
              <ul role="list" class="-my-4 divide-y divide-zinc-600">
                <li v-for="post in trendingPosts" :key="post.id" class="flex py-4 space-x-3">
                  <div class="flex-shrink-0">
                    <img class="h-8 w-8 rounded-full" :src="post.user.imageUrl" :alt="post.user.name"/>
                  </div>
                  <div class="min-w-0 flex-1">
                    <p class="text-sm text-zinc-200">{{ post.body }}</p>
                    <div class="mt-2 flex">
                      <span class="inline-flex items-center text-sm">
                          <button type="button" class="inline-flex space-x-2 text-zinc-400 hover:text-zinc-200">
                            <ChatAltIcon class="h-5 w-5" aria-hidden="true"/>
                            <span class="font-medium text-zinc-100">{{ post.comments }}</span>
                          </button>
                        </span>
                    </div>
                  </div>
                </li>
              </ul>
            </AsideSection>
        </Aside>
      </div>
    </div>
  </div>
</template>

<script setup>
import {
  ChatAltIcon,
  PlusSmIcon,
} from '@heroicons/vue/solid'
import {FireIcon, HomeIcon, TrendingUpIcon, UserGroupIcon} from '@heroicons/vue/outline'
import Navigation from "@/components/Navigation.vue";
import Sidebar from "@/components/Sidebar.vue";
import Tabs from "@/components/Tabs.vue";
import AsideSection from "@/components/AsideSection.vue";
import Aside from "@/components/Aside.vue";

const user = {
  name: 'Chelsea Hagon',
  email: 'chelseahagon@example.com',
  imageUrl:
      'https://images.unsplash.com/photo-1550525811-e5869dd03032?ixlib=rb-1.2.1&ixid=eyJhcHBfaWQiOjEyMDd9&auto=format&fit=facearea&facepad=2&w=256&h=256&q=80',
}

const navigation = [
  {name: 'Home', href: '#', icon: HomeIcon, current: true},
  {name: 'Popular', href: '#', icon: FireIcon, current: false},
  {name: 'Communities', href: '#', icon: UserGroupIcon, current: false},
  {name: 'Trending', href: '#', icon: TrendingUpIcon, current: false},
]

const tabs = [
  {name: 'Recent', href: '#', current: true},
  {name: 'Most Liked', href: '#', current: false},
  {name: 'Most Answers', href: '#', current: false},
]
const questions = [
  {
    id: '81614',
    likes: '29',
    replies: '11',
    views: '2.7k',
    author: {
      name: 'Dries Vincent',
      imageUrl:
          'https://images.unsplash.com/photo-1506794778202-cad84cf45f1d?ixlib=rb-1.2.1&ixid=eyJhcHBfaWQiOjEyMDd9&auto=format&fit=facearea&facepad=2&w=256&h=256&q=80',
      href: '#',
    },
    date: 'December 9 at 11:43 AM',
    datetime: '2020-12-09T11:43:00',
    href: '#',
    title: 'What would you have done differently if you ran Jurassic Park?',
    body: `
      <p>Jurassic Park was an incredible idea and a magnificent feat of engineering, but poor protocols and a disregard for human safety killed what could have otherwise been one of the best businesses of our generation.</p>
      <p>Ultimately, I think that if you wanted to run the park successfully and keep visitors safe, the most important thing to prioritize would be&hellip;</p>
    `,
  },
  {
    id: '42',
    likes: '123',
    replies: '54',
    views: '25.4k',
    author: {
      name: 'James Thrown',
      imageUrl:
          'https://images.unsplash.com/photo-1463453091185-61582044d556?ixlib=rb-1.2.1&ixid=eyJhcHBfaWQiOjEyMDd9&auto=format&fit=facearea&facepad=2&w=256&h=256&q=80',
      href: '#',
    },
    date: 'January 12 at 17:32 AM',
    datetime: '2022-01-12T17:32:00',
    href: '#',
    title: 'Why did the chicken cross the road?',
    body: `
      <p>This question implies that the chicken did, in fact, cross the road. However, it did not.</p>
      <p>A chicken would not have the mental capacity to rationalize the difference between a field and a road!</p>
    `,
  },
  {
    id: '42',
    likes: '123',
    replies: '54',
    views: '25.4k',
    author: {
      name: 'James Thrown',
      imageUrl:
          'https://images.unsplash.com/photo-1463453091185-61582044d556?ixlib=rb-1.2.1&ixid=eyJhcHBfaWQiOjEyMDd9&auto=format&fit=facearea&facepad=2&w=256&h=256&q=80',
      href: '#',
    },
    date: 'January 12 at 17:32 AM',
    datetime: '2022-01-12T17:32:00',
    href: '#',
    title: 'Why did the chicken cross the road?',
    body: `
      <p>This question implies that the chicken did, in fact, cross the road. However, it did not.</p>
      <p>A chicken would not have the mental capacity to rationalize the difference between a field and a road!</p>
    `,
  },
  {
    id: '42',
    likes: '123',
    replies: '54',
    views: '25.4k',
    author: {
      name: 'James Thrown',
      imageUrl:
          'https://images.unsplash.com/photo-1463453091185-61582044d556?ixlib=rb-1.2.1&ixid=eyJhcHBfaWQiOjEyMDd9&auto=format&fit=facearea&facepad=2&w=256&h=256&q=80',
      href: '#',
    },
    date: 'January 12 at 17:32 AM',
    datetime: '2022-01-12T17:32:00',
    href: '#',
    title: 'Why did the chicken cross the road?',
    body: `
      <p>This question implies that the chicken did, in fact, cross the road. However, it did not.</p>
      <p>A chicken would not have the mental capacity to rationalize the difference between a field and a road!</p>
    `,
  },
]
const whoToFollow = [
  {
    name: 'Leonard Krasner',
    handle: 'leonardkrasner',
    href: '#',
    imageUrl:
        'https://images.unsplash.com/photo-1519345182560-3f2917c472ef?ixlib=rb-1.2.1&ixid=eyJhcHBfaWQiOjEyMDd9&auto=format&fit=facearea&facepad=2&w=256&h=256&q=80',
  },
  {
    name: 'Leonard Krasner',
    handle: 'leonardkrasner',
    href: '#',
    imageUrl:
        'https://images.unsplash.com/photo-1519345182560-3f2917c472ef?ixlib=rb-1.2.1&ixid=eyJhcHBfaWQiOjEyMDd9&auto=format&fit=facearea&facepad=2&w=256&h=256&q=80',
  },
  // More people...
]
const trendingPosts = [
  {
    id: 1,
    user: {
      name: 'Floyd Miles',
      imageUrl:
          'https://images.unsplash.com/photo-1463453091185-61582044d556?ixlib=rb-1.2.1&ixid=eyJhcHBfaWQiOjEyMDd9&auto=format&fit=facearea&facepad=2&w=256&h=256&q=80',
    },
    body: 'What books do you have on your bookshelf just to look smarter than you actually are?',
    comments: 291,
  },
  {
    id: 2,
    user: {
      name: 'Jim Davies',
      imageUrl:
          'https://images.unsplash.com/photo-1531427186611-ecfd6d936c79?ixlib=rb-1.2.1&ixid=eyJhcHBfaWQiOjEyMDd9&auto=format&fit=facearea&facepad=2&w=256&h=256&q=80',
    },
    body: 'The quick brown fox jumps over the lazy dogs',
    comments: 43,
  },
  // More posts...
]

</script>