<template>
  <div class="overflow-hidden rounded-lg bg-white shadow-sm">
    <h2 class="sr-only" id="profile-overview-title">Profile Overview</h2>
    <div class="bg-white p-6">
      <div class="sm:flex sm:items-center sm:justify-between">
        <div class="sm:flex sm:space-x-5">
          <div class="shrink-0">
            <img class="mx-auto size-20 rounded-full" :src="user.imageUrl" alt="" />
          </div>
          <div class="mt-4 text-center sm:mt-0 sm:pt-1 sm:text-left">
            <p class="text-sm font-medium text-gray-600">Welcome back,</p>
            <p class="text-xl font-bold text-gray-900 sm:text-2xl">{{ user.name }}</p>
            <p class="text-sm font-medium text-gray-600">{{ user.role }}</p>
          </div>
        </div>
        <div class="mt-5 flex justify-center sm:mt-0">
          <a href="#" class="flex items-center justify-center rounded-md bg-white px-3 py-2 text-sm font-semibold text-gray-900 ring-1 shadow-xs ring-gray-300 ring-inset hover:bg-gray-50">View profile</a>
        </div>
      </div>
    </div>
    <div class="grid grid-cols-1 divide-y divide-gray-200 border-t border-gray-200 bg-gray-50 sm:grid-cols-3 sm:divide-x sm:divide-y-0">
      <div v-for="stat in stats" :key="stat.label" class="px-6 py-5 text-center text-sm font-medium">
        <span class="text-gray-900">{{ stat.value }}</span>
        {{ ' ' }}
        <span class="text-gray-600">{{ stat.label }}</span>
      </div>
    </div>
  </div>
</template>

<script setup>
const user = {
  name: 'Rebecca Nicholas',
  role: 'Product Designer',
  imageUrl:
    'https://images.unsplash.com/photo-1550525811-e5869dd03032?ixlib=rb-1.2.1&ixid=eyJhcHBfaWQiOjEyMDd9&auto=format&fit=facearea&facepad=2&w=256&h=256&q=80',
}
const stats = [
  { label: 'Vacation days left', value: 12 },
  { label: 'Sick days left', value: 4 },
  { label: 'Personal days left', value: 2 },
]
</script>