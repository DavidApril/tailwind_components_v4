<template>
  <div class="border-l-4 border-yellow-400 bg-yellow-50 p-4">
    <div class="flex">
      <div class="shrink-0">
        <ExclamationTriangleIcon class="size-5 text-yellow-400" aria-hidden="true" />
      </div>
      <div class="ml-3">
        <p class="text-sm text-yellow-700">
          You have no credits left.
          {{ ' ' }}
          <a href="#" class="font-medium text-yellow-700 underline hover:text-yellow-600">Upgrade your account to add more credits.</a>
        </p>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ExclamationTriangleIcon } from '@heroicons/vue/20/solid'
</script>