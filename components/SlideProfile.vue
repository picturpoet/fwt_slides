<script setup lang="ts">
interface PastWorkItem {
  label: string
  bg: string
  color: string
}

defineProps<{
  name: string
  photoUrl?: string
  punchlineHTML: string
  context: string
  expertise: string[]
  pastWork: PastWorkItem[]
}>()
</script>

<template>
<div class="flex h-full items-center gap-12 px-4">
  <div class="w-1/3 flex justify-center">
    <!-- Photo Area -->
    <div class="relative w-72 h-72 rounded-full border-4 border-gray-200 dark:border-gray-700 overflow-hidden shadow-2xl bg-gray-100 dark:bg-gray-800 flex items-center justify-center">
        <img v-if="photoUrl" :src="photoUrl" alt="Profile Photo" class="w-full h-full object-cover" />
        <span v-else class="text-6xl opacity-30">📷</span>
        <div v-if="!photoUrl" class="absolute bottom-4 left-0 right-0 text-center text-xs opacity-50">Place Photo Here</div>
    </div>
  </div>

  <div class="w-2/3 flex flex-col justify-center">
    <h1 class="text-6xl font-bold mb-4 bg-clip-text text-transparent bg-gradient-to-r from-blue-600 to-teal-500">
      {{ name }}
    </h1>
    
    <div class="text-2xl font-light mb-8 text-gray-700 dark:text-gray-300 leading-snug" v-html="punchlineHTML"></div>

    <div class="space-y-6">
      <div class="pl-4 border-l-4 border-gray-300 dark:border-gray-600">
        <div class="text-sm font-bold uppercase tracking-wider text-gray-500 mb-1">FWT Context</div>
        <div class="text-lg">
          {{ context }}
        </div>
      </div>
      
      <div>
        <div class="text-sm font-bold uppercase tracking-wider text-gray-500 mb-2">Expertise</div>
        <div class="flex gap-2">
            <span v-for="item in expertise" :key="item" class="px-3 py-1 bg-gray-100 dark:bg-gray-800 rounded-md text-sm ring-1 ring-gray-200 dark:ring-gray-700">
              {{ item }}
            </span>
        </div>
      </div>

       <div>
        <div class="text-sm font-bold uppercase tracking-wider text-gray-500 mb-2">Past Work</div>
        <div class="flex flex-wrap gap-3 items-center">
           <span v-for="work in pastWork" :key="work.label" 
                 class="px-3 py-1.5 font-bold rounded text-sm shadow-sm"
                 :style="{ backgroundColor: work.bg, color: work.color }">
             {{ work.label }}
           </span>
        </div>
      </div>
    </div>
  </div>
</div>
</template>
