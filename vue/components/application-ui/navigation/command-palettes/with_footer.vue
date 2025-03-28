<template>
  <TransitionRoot :show="open" as="template" @after-leave="rawQuery = ''" appear>
    <Dialog class="relative z-10" @close="open = false">
      <TransitionChild as="template" enter="ease-out duration-300" enter-from="opacity-0" enter-to="opacity-100" leave="ease-in duration-200" leave-from="opacity-100" leave-to="opacity-0">
        <div class="fixed inset-0 bg-gray-500/25 transition-opacity" />
      </TransitionChild>

      <div class="fixed inset-0 z-10 w-screen overflow-y-auto p-4 sm:p-6 md:p-20">
        <TransitionChild as="template" enter="ease-out duration-300" enter-from="opacity-0 scale-95" enter-to="opacity-100 scale-100" leave="ease-in duration-200" leave-from="opacity-100 scale-100" leave-to="opacity-0 scale-95">
          <DialogPanel class="mx-auto max-w-xl transform divide-y divide-gray-100 overflow-hidden rounded-xl bg-white ring-1 shadow-2xl ring-black/5 transition-all">
            <Combobox @update:modelValue="onSelect">
              <div class="grid grid-cols-1">
                <ComboboxInput class="col-start-1 row-start-1 h-12 w-full pr-4 pl-11 text-base text-gray-900 outline-hidden placeholder:text-gray-400 sm:text-sm" placeholder="Search..." @change="rawQuery = $event.target.value" @blur="query = ''" />
                <MagnifyingGlassIcon class="pointer-events-none col-start-1 row-start-1 ml-4 size-5 self-center text-gray-400" aria-hidden="true" />
              </div>

              <ComboboxOptions v-if="filteredProjects.length > 0 || filteredUsers.length > 0" static as="ul" class="max-h-80 transform-gpu scroll-py-10 scroll-pb-2 space-y-4 overflow-y-auto p-4 pb-2">
                <li v-if="filteredProjects.length > 0">
                  <h2 class="text-xs font-semibold text-gray-900">Projects</h2>
                  <ul class="-mx-4 mt-2 text-sm text-gray-700">
                    <ComboboxOption v-for="project in filteredProjects" :key="project.id" :value="project" as="template" v-slot="{ active }">
                      <li :class="['flex cursor-default items-center px-4 py-2 select-none', active && 'bg-indigo-600 text-white outline-hidden']">
                        <FolderIcon :class="['size-6 flex-none', active ? 'text-white forced-colors:text-[Highlight]' : 'text-gray-400']" aria-hidden="true" />
                        <span class="ml-3 flex-auto truncate">{{ project.name }}</span>
                      </li>
                    </ComboboxOption>
                  </ul>
                </li>
                <li v-if="filteredUsers.length > 0">
                  <h2 class="text-xs font-semibold text-gray-900">Users</h2>
                  <ul class="-mx-4 mt-2 text-sm text-gray-700">
                    <ComboboxOption v-for="user in filteredUsers" :key="user.id" :value="user" as="template" v-slot="{ active }">
                      <li :class="['flex cursor-default items-center px-4 py-2 select-none', active && 'bg-indigo-600 text-white outline-hidden']">
                        <img :src="user.imageUrl" alt="" class="size-6 flex-none rounded-full" />
                        <span class="ml-3 flex-auto truncate">{{ user.name }}</span>
                      </li>
                    </ComboboxOption>
                  </ul>
                </li>
              </ComboboxOptions>

              <div v-if="rawQuery === '?'" class="px-6 py-14 text-center text-sm sm:px-14">
                <LifebuoyIcon class="mx-auto size-6 text-gray-400" aria-hidden="true" />
                <p class="mt-4 font-semibold text-gray-900">Help with searching</p>
                <p class="mt-2 text-gray-500">Use this tool to quickly search for users and projects across our entire platform. You can also use the search modifiers found in the footer below to limit the results to just users or projects.</p>
              </div>

              <div v-if="query !== '' && rawQuery !== '?' && filteredProjects.length === 0 && filteredUsers.length === 0" class="px-6 py-14 text-center text-sm sm:px-14">
                <ExclamationTriangleIcon class="mx-auto size-6 text-gray-400" aria-hidden="true" />
                <p class="mt-4 font-semibold text-gray-900">No results found</p>
                <p class="mt-2 text-gray-500">We couldn’t find anything with that term. Please try again.</p>
              </div>

              <div class="flex flex-wrap items-center bg-gray-50 px-4 py-2.5 text-xs text-gray-700">
                Type
                <kbd :class="['mx-1 flex size-5 items-center justify-center rounded-sm border bg-white font-semibold sm:mx-2', rawQuery.startsWith('#') ? 'border-indigo-600 text-indigo-600' : 'border-gray-400 text-gray-900']">#</kbd>
                <span class="sm:hidden">for projects,</span>
                <span class="hidden sm:inline">to access projects,</span>
                <kbd :class="['mx-1 flex size-5 items-center justify-center rounded-sm border bg-white font-semibold sm:mx-2', rawQuery.startsWith('>') ? 'border-indigo-600 text-indigo-600' : 'border-gray-400 text-gray-900']">&gt;</kbd>
                for users, and
                <kbd :class="['mx-1 flex size-5 items-center justify-center rounded-sm border bg-white font-semibold sm:mx-2', rawQuery === '?' ? 'border-indigo-600 text-indigo-600' : 'border-gray-400 text-gray-900']">?</kbd>
                for help.
              </div>
            </Combobox>
          </DialogPanel>
        </TransitionChild>
      </div>
    </Dialog>
  </TransitionRoot>
</template>

<script setup>
import { computed, ref } from 'vue'
import { MagnifyingGlassIcon } from '@heroicons/vue/20/solid'
import { ExclamationTriangleIcon, FolderIcon, LifebuoyIcon } from '@heroicons/vue/24/outline'
import {
  Combobox,
  ComboboxInput,
  ComboboxOptions,
  ComboboxOption,
  Dialog,
  DialogPanel,
  TransitionChild,
  TransitionRoot,
} from '@headlessui/vue'

const projects = [
  { id: 1, name: 'Workflow Inc. / Website Redesign', category: 'Projects', url: '#' },
  // More projects...
]

const users = [
  {
    id: 1,
    name: 'Leslie Alexander',
    url: '#',
    imageUrl:
      'https://images.unsplash.com/photo-1494790108377-be9c29b29330?ixlib=rb-1.2.1&ixid=eyJhcHBfaWQiOjEyMDd9&auto=format&fit=facearea&facepad=2&w=256&h=256&q=80',
  },
  // More users...
]

const open = ref(true)
const rawQuery = ref('')
const query = computed(() => rawQuery.value.toLowerCase().replace(/^[#>]/, ''))
const filteredProjects = computed(() =>
  rawQuery.value === '#'
    ? projects
    : query.value === '' || rawQuery.value.startsWith('>')
      ? []
      : projects.filter((project) => project.name.toLowerCase().includes(query.value)),
)
const filteredUsers = computed(() =>
  rawQuery.value === '>'
    ? users
    : query.value === '' || rawQuery.value.startsWith('#')
      ? []
      : users.filter((user) => user.name.toLowerCase().includes(query.value)),
)

function onSelect(item) {
  if (item) {
    window.location = item.url
  }
}
</script>