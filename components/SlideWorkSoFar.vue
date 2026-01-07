<template>
  <div class="h-full w-full flex flex-col justify-center px-6 py-4 text-white relative overflow-hidden">
    <!-- Background Blur Effect -->
    <div class="absolute -top-20 -right-20 w-96 h-96 bg-blue-500 rounded-full mix-blend-multiply filter blur-3xl opacity-10 animate-blob"></div>
    <div class="absolute -bottom-20 -left-20 w-96 h-96 bg-purple-500 rounded-full mix-blend-multiply filter blur-3xl opacity-10 animate-blob animation-delay-2000"></div>

    <h1 class="text-3xl font-bold mb-1 z-10">Progress So Far</h1>
    <p class="text-lg opacity-70 mb-3 z-10">Over 20 hours spent to take us from initial conversations to concrete execution plans.</p>

    <div class="relative z-10 flex-1 flex flex-col" style="max-height: calc(100% - 100px)">
      <!-- Connection Line -->
      <svg class="absolute inset-0 w-full h-full" style="pointer-events: none;">
        <path d="M 10% 85%, L 30% 65%, L 50% 45%, L 70% 25%, L 90% 5%"
              stroke="url(#gradient)"
              stroke-width="2"
              fill="none"
              opacity="0.3"
              stroke-linecap="round"/>
        <defs>
          <linearGradient id="gradient" x1="0%" y1="0%" x2="100%" y2="0%">
            <stop offset="0%" style="stop-color:#3b82f6"/>
            <stop offset="25%" style="stop-color:#a855f7"/>
            <stop offset="50%" style="stop-color:#f97316"/>
            <stop offset="75%" style="stop-color:#ec4899"/>
            <stop offset="100%" style="stop-color:#22c55e"/>
          </linearGradient>
        </defs>
      </svg>

      <div class="grid grid-cols-5 gap-2.5 flex-1 items-end" style="min-height: 0">
        <!-- Column 1 - Lowest -->
        <div v-click class="relative group" style="margin-bottom: 30px">
          <div class="absolute -top-2 left-1/2 w-3 h-3 bg-blue-500 rounded-full transform -translate-x-1/2 ring-4 ring-slate-900 z-20"></div>
          <div class="p-3 bg-slate-800/80 backdrop-blur-md rounded-lg border border-slate-700 hover:border-blue-500/50 transition-all duration-300 hover:shadow-lg hover:shadow-blue-500/10 h-40 flex flex-col shadow-xl">
            <div class="text-blue-400 font-mono text-[10px] mb-1">Mid Nov</div>
            <h3 class="font-bold text-sm mb-1.5">Scope Architecture</h3>
            <p class="text-[10px] opacity-80 leading-tight mb-1.5">
              3 sessions with Yakub Ali, GVG & Loganathan.
            </p>
            <div class="mt-auto pt-1.5 border-t border-slate-700/50 text-[9px] opacity-60">
              AI powered logistics improvements
            </div>
          </div>
        </div>

        <!-- Column 2 -->
        <div v-click class="relative group" style="margin-bottom: 60px">
          <div class="absolute -top-2 left-1/2 w-3 h-3 bg-purple-500 rounded-full transform -translate-x-1/2 ring-4 ring-slate-900 z-20"></div>
          <div class="p-3 bg-slate-800/80 backdrop-blur-md rounded-lg border border-slate-700 hover:border-purple-500/50 transition-all duration-300 hover:shadow-lg hover:shadow-purple-500/10 h-40 flex flex-col shadow-xl">
            <div class="text-purple-400 font-mono text-[10px] mb-1">End Nov - Dec 7th</div>
            <h3 class="font-bold text-sm mb-1.5">Deep Dive & Data</h3>
            <p class="text-[10px] opacity-80 leading-tight mb-1.5">
              3 meetings with GVG, Md. Sulaiman, & Loganathan respectively covering data, workflows & tech stack.
            </p>
            <div class="mt-auto pt-1.5 border-t border-slate-700/50 text-[9px] opacity-60">
              Mapped workflows, data structures & tech integrations.
            </div>
          </div>
        </div>

        <!-- Column 3 -->
        <div v-click class="relative group" style="margin-bottom: 90px">
          <div class="absolute -top-2 left-1/2 w-3 h-3 bg-orange-500 rounded-full transform -translate-x-1/2 ring-4 ring-slate-900 z-20"></div>
          <div class="p-3 bg-slate-800/80 backdrop-blur-md rounded-lg border border-slate-700 hover:border-orange-500/50 transition-all duration-300 hover:shadow-lg hover:shadow-orange-500/10 h-40 flex flex-col shadow-xl">
            <div class="text-orange-400 font-mono text-[10px] mb-1">Dec 7 - 15</div>
            <h3 class="font-bold text-sm mb-1.5">Scope Evolution</h3>
            <p class="text-[10px] opacity-80 leading-tight mb-1.5">
              Driver app improvements identified for system enhancement.
            </p>
            <div class="mt-auto pt-1.5 border-t border-slate-700/50 text-[9px] flex gap-1">
              <span class="px-1 py-0.5 bg-pink-500/20 rounded text-pink-300">Eagle</span>
              <span class="px-1 py-0.5 bg-red-500/20 rounded text-red-300">HotWheels</span>
            </div>
          </div>
        </div>

        <!-- Column 4 -->
        <div v-click class="relative group" style="margin-bottom: 120px">
          <div class="absolute -top-2 left-1/2 w-3 h-3 bg-pink-500 rounded-full transform -translate-x-1/2 ring-4 ring-slate-900 z-20"></div>
          <div class="p-3 bg-slate-800/80 backdrop-blur-md rounded-lg border border-slate-700 hover:border-pink-500/50 transition-all duration-300 hover:shadow-lg hover:shadow-pink-500/10 h-40 flex flex-col shadow-xl">
            <div class="text-pink-400 font-mono text-[10px] mb-1">Dec 15 - 30</div>
            <h3 class="font-bold text-sm mb-1.5">Rapid Prototyping</h3>
            <p class="text-[10px] opacity-80 leading-tight mb-1.5">
              2 sessions where stakeholders saw close-to-final UX.
            </p>
            <div class="mt-auto pt-1.5 border-t border-slate-700/50 text-[9px] opacity-60">
              Interactive prototypes brought vision to life.
            </div>
          </div>
        </div>

        <!-- Column 5 - Highest -->
        <div v-click class="relative group" style="margin-bottom: 150px">
          <div class="absolute -top-2 left-1/2 w-3 h-3 bg-green-500 rounded-full transform -translate-x-1/2 ring-4 ring-slate-900 z-20 animate-pulse"></div>
          <div class="p-3 bg-gradient-to-b from-green-900/30 to-slate-800/80 backdrop-blur-md rounded-lg border border-green-500/30 hover:border-green-400/80 transition-all duration-300 hover:shadow-lg hover:shadow-green-500/20 h-40 flex flex-col shadow-xl justify-center items-center text-center">
            <div class="text-2xl mb-1.5">🚀</div>
            <h3 class="font-bold text-base mb-1 text-green-400">Ready to Launch</h3>
            <p class="text-[10px] opacity-80">
              Awaiting Approval & Kickoff
            </p>
          </div>
        </div>
      </div>

      <!-- Timeline Axis -->
      <div class="mt-6 relative flex-shrink-0">
        <!-- Main axis line -->
        <div class="absolute left-0 right-0 top-3 h-0.5 bg-gradient-to-r from-slate-600 via-slate-500 to-slate-600 opacity-50"></div>

        <!-- Timeline markers -->
        <div class="grid grid-cols-5 gap-2.5 relative">
          <div class="flex flex-col items-center">
            <div class="w-2 h-2 bg-blue-500 rounded-full ring-2 ring-slate-900 mb-1"></div>
            <span class="text-[10px] font-mono text-slate-400">Mid Nov</span>
          </div>
          <div class="flex flex-col items-center">
            <div class="w-2 h-2 bg-purple-500 rounded-full ring-2 ring-slate-900 mb-1"></div>
            <span class="text-[10px] font-mono text-slate-400">End Nov - 7th Dec</span>
          </div>
          <div class="flex flex-col items-center">
            <div class="w-2 h-2 bg-orange-500 rounded-full ring-2 ring-slate-900 mb-1"></div>
            <span class="text-[10px] font-mono text-slate-400">Dec 7-15</span>
          </div>
          <div class="flex flex-col items-center">
            <div class="w-2 h-2 bg-pink-500 rounded-full ring-2 ring-slate-900 mb-1"></div>
            <span class="text-[10px] font-mono text-slate-400">Dec 15-30</span>
          </div>
          <div class="flex flex-col items-center">
            <div class="w-2 h-2 bg-green-500 rounded-full ring-2 ring-slate-900 mb-1 animate-pulse"></div>
            <span class="text-[10px] font-mono text-green-400">Jan Week 1</span>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<style scoped>
.animate-blob {
  animation: blob 7s infinite;
}
.animation-delay-2000 {
  animation-delay: 2s;
}
@keyframes blob {
  0% { transform: translate(0px, 0px) scale(1); }
  33% { transform: translate(30px, -50px) scale(1.1); }
  66% { transform: translate(-20px, 20px) scale(0.9); }
  100% { transform: translate(0px, 0px) scale(1); }
}
</style>
