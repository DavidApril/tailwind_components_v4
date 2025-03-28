<template>
  <ul role="list" class="space-y-6">
    <li v-for="(activityItem, activityItemIdx) in activity" :key="activityItem.id" class="relative flex gap-x-4">
      <div :class="[activityItemIdx === activity.length - 1 ? 'h-6' : '-bottom-6', 'absolute top-0 left-0 flex w-6 justify-center']">
        <div class="w-px bg-gray-200" />
      </div>
      <template v-if="activityItem.type === 'commented'">
        <img :src="activityItem.person.imageUrl" alt="" class="relative mt-3 size-6 flex-none rounded-full bg-gray-50" />
        <div class="flex-auto rounded-md p-3 ring-1 ring-gray-200 ring-inset">
          <div class="flex justify-between gap-x-4">
            <div class="py-0.5 text-xs/5 text-gray-500">
              <span class="font-medium text-gray-900">{{ activityItem.person.name }}</span> commented
            </div>
            <time :datetime="activityItem.dateTime" class="flex-none py-0.5 text-xs/5 text-gray-500">{{ activityItem.date }}</time>
          </div>
          <p class="text-sm/6 text-gray-500">{{ activityItem.comment }}</p>
        </div>
      </template>
      <template v-else>
        <div class="relative flex size-6 flex-none items-center justify-center bg-white">
          <CheckCircleIcon v-if="activityItem.type === 'paid'" class="size-6 text-indigo-600" aria-hidden="true" />
          <div v-else class="size-1.5 rounded-full bg-gray-100 ring-1 ring-gray-300" />
        </div>
        <p class="flex-auto py-0.5 text-xs/5 text-gray-500">
          <span class="font-medium text-gray-900">{{ activityItem.person.name }}</span> {{ activityItem.type }} the invoice.
        </p>
        <time :datetime="activityItem.dateTime" class="flex-none py-0.5 text-xs/5 text-gray-500">{{ activityItem.date }}</time>
      </template>
    </li>
  </ul>

  <!-- New comment form -->
  <div class="mt-6 flex gap-x-3">
    <img src="https://images.unsplash.com/photo-1472099645785-5658abf4ff4e?ixlib=rb-1.2.1&ixid=eyJhcHBfaWQiOjEyMDd9&auto=format&fit=facearea&facepad=2&w=256&h=256&q=80" alt="" class="size-6 flex-none rounded-full bg-gray-50" />
    <form action="#" class="relative flex-auto">
      <div class="overflow-hidden rounded-lg pb-12 outline-1 -outline-offset-1 outline-gray-300 focus-within:outline-2 focus-within:-outline-offset-2 focus-within:outline-indigo-600">
        <label for="comment" class="sr-only">Add your comment</label>
        <textarea rows="2" name="comment" id="comment" class="block w-full resize-none bg-transparent px-3 py-1.5 text-base text-gray-900 placeholder:text-gray-400 focus:outline-none sm:text-sm/6" placeholder="Add your comment..." />
      </div>

      <div class="absolute inset-x-0 bottom-0 flex justify-between py-2 pr-2 pl-3">
        <div class="flex items-center space-x-5">
          <div class="flex items-center">
            <button type="button" class="-m-2.5 flex size-10 items-center justify-center rounded-full text-gray-400 hover:text-gray-500">
              <PaperClipIcon class="size-5" aria-hidden="true" />
              <span class="sr-only">Attach a file</span>
            </button>
          </div>
          <div class="flex items-center">
            <Listbox as="div" v-model="selected">
              <ListboxLabel class="sr-only">Your mood</ListboxLabel>
              <div class="relative">
                <ListboxButton class="relative -m-2.5 flex size-10 items-center justify-center rounded-full text-gray-400 hover:text-gray-500">
                  <span class="flex items-center justify-center">
                    <span v-if="selected.value === null">
                      <FaceSmileIcon class="size-5 shrink-0" aria-hidden="true" />
                      <span class="sr-only">Add your mood</span>
                    </span>
                    <span v-if="!(selected.value === null)">
                      <span :class="[selected.bgColor, 'flex size-8 items-center justify-center rounded-full']">
                        <component :is="selected.icon" class="size-5 shrink-0 text-white" aria-hidden="true" />
                      </span>
                      <span class="sr-only">{{ selected.name }}</span>
                    </span>
                  </span>
                </ListboxButton>

                <transition leave-active-class="transition ease-in duration-100" leave-from-class="opacity-100" leave-to-class="opacity-0">
                  <ListboxOptions class="absolute bottom-10 z-10 -ml-6 w-60 rounded-lg bg-white py-3 text-base ring-1 shadow-sm ring-black/5 focus:outline-hidden sm:ml-auto sm:w-64 sm:text-sm">
                    <ListboxOption as="template" v-for="mood in moods" :key="mood.value" :value="mood" v-slot="{ active }">
                      <li :class="[active ? 'bg-gray-100' : 'bg-white', 'relative cursor-default px-3 py-2 select-none']">
                        <div class="flex items-center">
                          <div :class="[mood.bgColor, 'flex size-8 items-center justify-center rounded-full']">
                            <component :is="mood.icon" :class="[mood.iconColor, 'size-5 shrink-0']" aria-hidden="true" />
                          </div>
                          <span class="ml-3 block truncate font-medium">{{ mood.name }}</span>
                        </div>
                      </li>
                    </ListboxOption>
                  </ListboxOptions>
                </transition>
              </div>
            </Listbox>
          </div>
        </div>
        <button type="submit" class="rounded-md bg-white px-2.5 py-1.5 text-sm font-semibold text-gray-900 ring-1 shadow-xs ring-gray-300 ring-inset hover:bg-gray-50">Comment</button>
      </div>
    </form>
  </div>
</template>

<script setup>
import { ref } from 'vue'
import { CheckCircleIcon } from '@heroicons/vue/24/solid'
import {
  FaceFrownIcon,
  FaceSmileIcon,
  FireIcon,
  HandThumbUpIcon,
  HeartIcon,
  PaperClipIcon,
  XMarkIcon,
} from '@heroicons/vue/20/solid'
import { Listbox, ListboxButton, ListboxLabel, ListboxOption, ListboxOptions } from '@headlessui/vue'

const activity = [
  { id: 1, type: 'created', person: { name: 'Chelsea Hagon' }, date: '7d ago', dateTime: '2023-01-23T10:32' },
  { id: 2, type: 'edited', person: { name: 'Chelsea Hagon' }, date: '6d ago', dateTime: '2023-01-23T11:03' },
  { id: 3, type: 'sent', person: { name: 'Chelsea Hagon' }, date: '6d ago', dateTime: '2023-01-23T11:24' },
  {
    id: 4,
    type: 'commented',
    person: {
      name: 'Chelsea Hagon',
      imageUrl:
        'https://images.unsplash.com/photo-1550525811-e5869dd03032?ixlib=rb-1.2.1&ixid=eyJhcHBfaWQiOjEyMDd9&auto=format&fit=facearea&facepad=2&w=256&h=256&q=80',
    },
    comment: 'Called client, they reassured me the invoice would be paid by the 25th.',
    date: '3d ago',
    dateTime: '2023-01-23T15:56',
  },
  { id: 5, type: 'viewed', person: { name: 'Alex Curren' }, date: '2d ago', dateTime: '2023-01-24T09:12' },
  { id: 6, type: 'paid', person: { name: 'Alex Curren' }, date: '1d ago', dateTime: '2023-01-24T09:20' },
]
const moods = [
  { name: 'Excited', value: 'excited', icon: FireIcon, iconColor: 'text-white', bgColor: 'bg-red-500' },
  { name: 'Loved', value: 'loved', icon: HeartIcon, iconColor: 'text-white', bgColor: 'bg-pink-400' },
  { name: 'Happy', value: 'happy', icon: FaceSmileIcon, iconColor: 'text-white', bgColor: 'bg-green-400' },
  { name: 'Sad', value: 'sad', icon: FaceFrownIcon, iconColor: 'text-white', bgColor: 'bg-yellow-400' },
  { name: 'Thumbsy', value: 'thumbsy', icon: HandThumbUpIcon, iconColor: 'text-white', bgColor: 'bg-blue-500' },
  { name: 'I feel nothing', value: null, icon: XMarkIcon, iconColor: 'text-gray-400', bgColor: 'bg-transparent' },
]

const selected = ref(moods[5])
</script>