<template>
  <div class="bg-white">
    <!-- Mobile filter dialog -->
    <TransitionRoot as="template" :show="open">
      <Dialog class="relative z-40 sm:hidden" @close="open = false">
        <TransitionChild as="template" enter="transition-opacity ease-linear duration-300" enter-from="opacity-0" enter-to="opacity-100" leave="transition-opacity ease-linear duration-300" leave-from="opacity-100" leave-to="opacity-0">
          <div class="fixed inset-0 bg-black/25" />
        </TransitionChild>

        <div class="fixed inset-0 z-40 flex">
          <TransitionChild as="template" enter="transition ease-in-out duration-300 transform" enter-from="translate-x-full" enter-to="translate-x-0" leave="transition ease-in-out duration-300 transform" leave-from="translate-x-0" leave-to="translate-x-full">
            <DialogPanel class="relative ml-auto flex size-full max-w-xs flex-col overflow-y-auto bg-white py-4 pb-12 shadow-xl">
              <div class="flex items-center justify-between px-4">
                <h2 class="text-lg font-medium text-gray-900">Filters</h2>
                <button type="button" class="-mr-2 flex size-10 items-center justify-center rounded-md bg-white p-2 text-gray-400" @click="open = false">
                  <span class="sr-only">Close menu</span>
                  <XMarkIcon class="size-6" aria-hidden="true" />
                </button>
              </div>

              <!-- Filters -->
              <form class="mt-4">
                <Disclosure as="div" v-for="section in filters" :key="section.name" class="border-t border-gray-200 px-4 py-6" v-slot="{ open }">
                  <h3 class="-mx-2 -my-3 flow-root">
                    <DisclosureButton class="flex w-full items-center justify-between bg-white px-2 py-3 text-sm text-gray-400">
                      <span class="font-medium text-gray-900">{{ section.name }}</span>
                      <span class="ml-6 flex items-center">
                        <ChevronDownIcon :class="[open ? '-rotate-180' : 'rotate-0', 'size-5 transform']" aria-hidden="true" />
                      </span>
                    </DisclosureButton>
                  </h3>
                  <DisclosurePanel class="pt-6">
                    <div class="space-y-6">
                      <div v-for="(option, optionIdx) in section.options" :key="option.value" class="flex gap-3">
                        <div class="flex h-5 shrink-0 items-center">
                          <div class="group grid size-4 grid-cols-1">
                            <input :id="`filter-mobile-${section.id}-${optionIdx}`" :name="`${section.id}[]`" :value="option.value" type="checkbox" :checked="option.checked" class="col-start-1 row-start-1 appearance-none rounded-sm border border-gray-300 bg-white checked:border-indigo-600 checked:bg-indigo-600 indeterminate:border-indigo-600 indeterminate:bg-indigo-600 focus-visible:outline-2 focus-visible:outline-offset-2 focus-visible:outline-indigo-600 disabled:border-gray-300 disabled:bg-gray-100 disabled:checked:bg-gray-100 forced-colors:appearance-auto" />
                            <svg class="pointer-events-none col-start-1 row-start-1 size-3.5 self-center justify-self-center stroke-white group-has-disabled:stroke-gray-950/25" viewBox="0 0 14 14" fill="none">
                              <path class="opacity-0 group-has-checked:opacity-100" d="M3 8L6 11L11 3.5" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" />
                              <path class="opacity-0 group-has-indeterminate:opacity-100" d="M3 7H11" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" />
                            </svg>
                          </div>
                        </div>
                        <label :for="`filter-mobile-${section.id}-${optionIdx}`" class="text-sm text-gray-500">{{ option.label }}</label>
                      </div>
                    </div>
                  </DisclosurePanel>
                </Disclosure>
              </form>
            </DialogPanel>
          </TransitionChild>
        </div>
      </Dialog>
    </TransitionRoot>

    <div class="mx-auto max-w-7xl px-4 py-16 sm:px-6 lg:px-8">
      <h1 class="text-3xl font-bold tracking-tight text-gray-900">Workspace sale</h1>
      <p class="mt-4 max-w-xl text-sm text-gray-700">Our thoughtfully designed workspace objects are crafted in limited runs. Improve your productivity and organization with these sale items before we run out.</p>
    </div>

    <!-- Filters -->
    <section aria-labelledby="filter-heading">
      <h2 id="filter-heading" class="sr-only">Filters</h2>

      <div class="border-b border-gray-200 bg-white pb-4">
        <div class="mx-auto flex max-w-7xl items-center justify-between px-4 sm:px-6 lg:px-8">
          <Menu as="div" class="relative inline-block text-left">
            <div>
              <MenuButton class="group inline-flex justify-center text-sm font-medium text-gray-700 hover:text-gray-900">
                Sort
                <ChevronDownIcon class="-mr-1 ml-1 size-5 shrink-0 text-gray-400 group-hover:text-gray-500" aria-hidden="true" />
              </MenuButton>
            </div>

            <transition enter-active-class="transition ease-out duration-100" enter-from-class="transform opacity-0 scale-95" enter-to-class="transform opacity-100 scale-100" leave-active-class="transition ease-in duration-75" leave-from-class="transform opacity-100 scale-100" leave-to-class="transform opacity-0 scale-95">
              <MenuItems class="absolute left-0 z-10 mt-2 w-40 origin-top-left rounded-md bg-white ring-1 shadow-2xl ring-black/5 focus:outline-hidden">
                <div class="py-1">
                  <MenuItem v-for="option in sortOptions" :key="option.name" v-slot="{ active }">
                    <a :href="option.href" :class="[option.current ? 'font-medium text-gray-900' : 'text-gray-500', active ? 'bg-gray-100 outline-hidden' : '', 'block px-4 py-2 text-sm']">{{ option.name }}</a>
                  </MenuItem>
                </div>
              </MenuItems>
            </transition>
          </Menu>

          <button type="button" class="inline-block text-sm font-medium text-gray-700 hover:text-gray-900 sm:hidden" @click="open = true">Filters</button>

          <div class="hidden sm:block">
            <div class="flow-root">
              <PopoverGroup class="-mx-4 flex items-center divide-x divide-gray-200">
                <Popover v-for="(section, sectionIdx) in filters" :key="section.name" class="relative inline-block px-4 text-left">
                  <PopoverButton class="group inline-flex justify-center text-sm font-medium text-gray-700 hover:text-gray-900">
                    <span>{{ section.name }}</span>
                    <span v-if="sectionIdx === 0" class="ml-1.5 rounded-sm bg-gray-200 px-1.5 py-0.5 text-xs font-semibold text-gray-700 tabular-nums">1</span>
                    <ChevronDownIcon class="-mr-1 ml-1 size-5 shrink-0 text-gray-400 group-hover:text-gray-500" aria-hidden="true" />
                  </PopoverButton>

                  <transition enter-active-class="transition ease-out duration-100" enter-from-class="transform opacity-0 scale-95" enter-to-class="transform opacity-100 scale-100" leave-active-class="transition ease-in duration-75" leave-from-class="transform opacity-100 scale-100" leave-to-class="transform opacity-0 scale-95">
                    <PopoverPanel class="absolute right-0 z-10 mt-2 origin-top-right rounded-md bg-white p-4 ring-1 shadow-2xl ring-black/5 focus:outline-hidden">
                      <form class="space-y-4">
                        <div v-for="(option, optionIdx) in section.options" :key="option.value" class="flex gap-3">
                          <div class="flex h-5 shrink-0 items-center">
                            <div class="group grid size-4 grid-cols-1">
                              <input :id="`filter-${section.id}-${optionIdx}`" :name="`${section.id}[]`" :value="option.value" type="checkbox" :checked="option.checked" class="col-start-1 row-start-1 appearance-none rounded-sm border border-gray-300 bg-white checked:border-indigo-600 checked:bg-indigo-600 indeterminate:border-indigo-600 indeterminate:bg-indigo-600 focus-visible:outline-2 focus-visible:outline-offset-2 focus-visible:outline-indigo-600 disabled:border-gray-300 disabled:bg-gray-100 disabled:checked:bg-gray-100 forced-colors:appearance-auto" />
                              <svg class="pointer-events-none col-start-1 row-start-1 size-3.5 self-center justify-self-center stroke-white group-has-disabled:stroke-gray-950/25" viewBox="0 0 14 14" fill="none">
                                <path class="opacity-0 group-has-checked:opacity-100" d="M3 8L6 11L11 3.5" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" />
                                <path class="opacity-0 group-has-indeterminate:opacity-100" d="M3 7H11" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" />
                              </svg>
                            </div>
                          </div>
                          <label :for="`filter-${section.id}-${optionIdx}`" class="pr-6 text-sm font-medium whitespace-nowrap text-gray-900">{{ option.label }}</label>
                        </div>
                      </form>
                    </PopoverPanel>
                  </transition>
                </Popover>
              </PopoverGroup>
            </div>
          </div>
        </div>
      </div>

      <!-- Active filters -->
      <div class="bg-gray-100">
        <div class="mx-auto max-w-7xl px-4 py-3 sm:flex sm:items-center sm:px-6 lg:px-8">
          <h3 class="text-sm font-medium text-gray-500">
            Filters
            <span class="sr-only">, active</span>
          </h3>

          <div aria-hidden="true" class="hidden h-5 w-px bg-gray-300 sm:ml-4 sm:block" />

          <div class="mt-2 sm:mt-0 sm:ml-4">
            <div class="-m-1 flex flex-wrap items-center">
              <span v-for="activeFilter in activeFilters" :key="activeFilter.value" class="m-1 inline-flex items-center rounded-full border border-gray-200 bg-white py-1.5 pr-2 pl-3 text-sm font-medium text-gray-900">
                <span>{{ activeFilter.label }}</span>
                <button type="button" class="ml-1 inline-flex size-4 shrink-0 rounded-full p-1 text-gray-400 hover:bg-gray-200 hover:text-gray-500">
                  <span class="sr-only">Remove filter for {{ activeFilter.label }}</span>
                  <svg class="size-2" stroke="currentColor" fill="none" viewBox="0 0 8 8">
                    <path stroke-linecap="round" stroke-width="1.5" d="M1 1l6 6m0-6L1 7" />
                  </svg>
                </button>
              </span>
            </div>
          </div>
        </div>
      </div>
    </section>
  </div>
</template>

<script setup>
import { ref } from 'vue'
import {
  Dialog,
  DialogPanel,
  Disclosure,
  DisclosureButton,
  DisclosurePanel,
  Menu,
  MenuButton,
  MenuItem,
  MenuItems,
  Popover,
  PopoverButton,
  PopoverGroup,
  PopoverPanel,
  TransitionChild,
  TransitionRoot,
} from '@headlessui/vue'
import { XMarkIcon } from '@heroicons/vue/24/outline'
import { ChevronDownIcon } from '@heroicons/vue/20/solid'

const sortOptions = [
  { name: 'Most Popular', href: '#', current: true },
  { name: 'Best Rating', href: '#', current: false },
  { name: 'Newest', href: '#', current: false },
]
const filters = [
  {
    id: 'category',
    name: 'Category',
    options: [
      { value: 'new-arrivals', label: 'All New Arrivals', checked: false },
      { value: 'tees', label: 'Tees', checked: false },
      { value: 'objects', label: 'Objects', checked: true },
    ],
  },
  {
    id: 'color',
    name: 'Color',
    options: [
      { value: 'white', label: 'White', checked: false },
      { value: 'beige', label: 'Beige', checked: false },
      { value: 'blue', label: 'Blue', checked: false },
    ],
  },
  {
    id: 'sizes',
    name: 'Sizes',
    options: [
      { value: 's', label: 'S', checked: false },
      { value: 'm', label: 'M', checked: false },
      { value: 'l', label: 'L', checked: false },
    ],
  },
]
const activeFilters = [{ value: 'objects', label: 'Objects' }]

const open = ref(false)
</script>