<template>
  <div class="relative bg-white">
    <div class="mx-auto max-w-7xl lg:flex lg:justify-between lg:px-8 xl:justify-end">
      <div class="lg:flex lg:w-1/2 lg:shrink lg:grow-0 xl:absolute xl:inset-y-0 xl:right-1/2 xl:w-1/2">
        <div class="relative h-80 lg:-ml-8 lg:h-auto lg:w-full lg:grow xl:ml-0">
          <img class="absolute inset-0 size-full bg-gray-50 object-cover" src="https://images.unsplash.com/photo-1559136555-9303baea8ebd?ixlib=rb-4.0.3&ixid=MnwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8&auto=format&fit=crop&crop=focalpoint&fp-x=.4&w=2560&h=3413&&q=80" alt="" />
        </div>
      </div>
      <div class="px-6 lg:contents">
        <div class="mx-auto max-w-2xl pt-16 pb-24 sm:pt-20 sm:pb-32 lg:mr-0 lg:ml-8 lg:w-full lg:max-w-lg lg:flex-none lg:pt-32 xl:w-1/2">
          <p class="text-base/7 font-semibold text-indigo-600">Deploy faster</p>
          <h1 class="mt-2 text-4xl font-semibold tracking-tight text-pretty text-gray-900 sm:text-5xl">A better workflow</h1>
          <p class="mt-6 text-xl/8 text-gray-700">Aliquet nec orci mattis amet quisque ullamcorper neque, nibh sem. At arcu, sit dui mi, nibh dui, diam eget aliquam. Quisque id at vitae feugiat egestas ac. Diam nulla orci at in viverra scelerisque eget. Eleifend egestas fringilla sapien.</p>
          <div class="mt-10 max-w-xl text-base/7 text-gray-700 lg:max-w-none">
            <p>Faucibus commodo massa rhoncus, volutpat. Dignissim sed eget risus enim. Mattis mauris semper sed amet vitae sed turpis id. Id dolor praesent donec est. Odio penatibus risus viverra tellus varius sit neque erat velit. Faucibus commodo massa rhoncus, volutpat. Dignissim sed eget risus enim. Mattis mauris semper sed amet vitae sed turpis id.</p>
            <ul role="list" class="mt-8 space-y-8 text-gray-600">
              <li class="flex gap-x-3">
                <CloudArrowUpIcon class="mt-1 size-5 flex-none text-indigo-600" aria-hidden="true" />
                <span><strong class="font-semibold text-gray-900">Push to deploy.</strong> Lorem ipsum, dolor sit amet consectetur adipisicing elit. Maiores impedit perferendis suscipit eaque, iste dolor cupiditate blanditiis ratione.</span>
              </li>
              <li class="flex gap-x-3">
                <LockClosedIcon class="mt-1 size-5 flex-none text-indigo-600" aria-hidden="true" />
                <span><strong class="font-semibold text-gray-900">SSL certificates.</strong> Anim aute id magna aliqua ad ad non deserunt sunt. Qui irure qui lorem cupidatat commodo.</span>
              </li>
              <li class="flex gap-x-3">
                <ServerIcon class="mt-1 size-5 flex-none text-indigo-600" aria-hidden="true" />
                <span><strong class="font-semibold text-gray-900">Database backups.</strong> Ac tincidunt sapien vehicula erat auctor pellentesque rhoncus. Et magna sit morbi lobortis.</span>
              </li>
            </ul>
            <p class="mt-8">Et vitae blandit facilisi magna lacus commodo. Vitae sapien duis odio id et. Id blandit molestie auctor fermentum dignissim. Lacus diam tincidunt ac cursus in vel. Mauris varius vulputate et ultrices hac adipiscing egestas. Iaculis convallis ac tempor et ut. Ac lorem vel integer orci.</p>
            <h2 class="mt-16 text-2xl font-bold tracking-tight text-gray-900">No server? No problem.</h2>
            <p class="mt-6">Id orci tellus laoreet id ac. Dolor, aenean leo, ac etiam consequat in. Convallis arcu ipsum urna nibh. Pharetra, euismod vitae interdum mauris enim, consequat vulputate nibh. Maecenas pellentesque id sed tellus mauris, ultrices mauris. Tincidunt enim cursus ridiculus mi. Pellentesque nam sed nullam sed diam turpis ipsum eu a sed convallis diam.</p>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
import { CloudArrowUpIcon, LockClosedIcon, ServerIcon } from '@heroicons/vue/20/solid'
</script>