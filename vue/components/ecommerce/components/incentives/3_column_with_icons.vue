<template>
  <div class="bg-white">
    <h2 class="sr-only">Why you should buy from us</h2>
    <div class="flex overflow-x-auto">
      <div class="mx-auto flex space-x-12 px-4 py-3 whitespace-nowrap sm:px-6 lg:space-x-24 lg:px-8">
        <div v-for="incentive in incentives" :key="incentive.name" class="flex items-center text-sm font-medium text-indigo-600">
          <component :is="incentive.icon" class="mr-2 size-6 flex-none" aria-hidden="true" />
          <p>{{ incentive.name }}</p>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
import { CalendarIcon, CheckBadgeIcon, TruckIcon } from '@heroicons/vue/24/outline'

const incentives = [
  { name: 'Free, contactless delivery', icon: TruckIcon },
  { name: 'No questions asked returns', icon: CheckBadgeIcon },
  { name: '2-year warranty', icon: CalendarIcon },
]
</script>