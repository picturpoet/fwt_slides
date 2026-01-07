<template>
  <div class="h-full flex flex-col items-center justify-center bg-white text-slate-900 p-6 overflow-hidden relative">
    
    <!-- Background Elements -->
    <div class="absolute top-0 left-0 w-full h-full overflow-hidden pointer-events-none">
      <div class="absolute top-10 left-10 w-64 h-64 bg-blue-500/5 rounded-full blur-3xl"></div>
      <div class="absolute bottom-10 right-10 w-64 h-64 bg-purple-500/5 rounded-full blur-3xl"></div>
    </div>

    <!-- Header -->
    <div class="text-center mb-2 relative z-10">
      <div class="text-xs font-bold tracking-[0.3em] text-blue-600 mb-2 uppercase">The 2026 Prediction</div>
      <h1 class="text-5xl font-black tracking-tight mb-2 bg-gradient-to-r from-blue-700 via-blue-600 to-blue-800 bg-clip-text text-transparent">
        OUR BIG BET
      </h1>
      <div class="text-lg text-gray-500 font-light italic">
        "The Great Separation"
      </div>
    </div>

    <!-- Main Content Area -->
    <div class="flex flex-col items-center w-full max-w-6xl relative z-10">
      
      <!-- Prediction Text -->
      <div class="text-center max-w-3xl mb-4">
        <p class="text-xl leading-relaxed text-gray-700 font-light">
          In <span class="font-bold text-slate-900">2026</span>, the companies that can implement AI within their <br>
          <span class="text-blue-700 border-b border-blue-500/30 pb-0.5 font-medium">existing workflows</span> will separate from those that don't.
        </p>
      </div>

      <!-- Visual Metaphor: The Marriage -->
      <div class="flex items-center justify-center w-full gap-6 mb-4">
        
        <!-- Pillar 1: System Design -->
        <div class="flex flex-col items-center group">
          <div class="w-48 h-32 rounded-2xl bg-white border border-gray-200 shadow-md flex flex-col items-center justify-center relative overflow-hidden transition-all duration-300 group-hover:border-blue-500 group-hover:shadow-[0_0_20px_rgba(59,130,246,0.15)]">
            <div class="absolute inset-0 bg-grid-slate-100/[0.5] bg-[length:16px_16px]"></div>
            <div class="text-4xl mb-2">🏗️</div>
            <div class="font-bold text-lg text-slate-800">System Design</div>
          </div>
        </div>

        <!-- The Marriage / Connection -->
        <div class="flex flex-col items-center relative px-4">
          <div class="absolute h-0.5 w-full top-1/2 bg-gradient-to-r from-transparent via-blue-300 to-transparent"></div>
          <div class="w-12 h-12 rounded-full bg-blue-600 flex items-center justify-center z-10 shadow-lg shadow-blue-600/30 text-xl text-white">
            🤝
          </div>
          <div class="mt-2 text-xs text-blue-600 font-bold tracking-wider uppercase">The Core Skill</div>
        </div>

        <!-- Pillar 2: Business Logic -->
         <div class="flex flex-col items-center group">
          <div class="w-48 h-32 rounded-2xl bg-white border border-gray-200 shadow-md flex flex-col items-center justify-center relative overflow-hidden transition-all duration-300 group-hover:border-purple-500 group-hover:shadow-[0_0_20px_rgba(168,85,247,0.15)]">
             <div class="absolute inset-0 bg-gradient-to-br from-purple-500/5 to-transparent"></div>
            <div class="text-4xl mb-2">💼</div>
            <div class="font-bold text-lg text-slate-800">Business Logic</div>
          </div>
        </div>

      </div>

      <!-- Key Feature: Flexibility -->
      <div class="relative group mt-2">
        <div class="absolute -inset-0.5 bg-gradient-to-r from-blue-500 to-purple-500 rounded-xl blur opacity-10 group-hover:opacity-30 transition duration-500"></div>
        <div class="relative px-8 py-4 bg-white ring-1 ring-gray-200 shadow-sm rounded-xl leading-none flex items-center">
          <div class="pr-4 border-r border-gray-200">
            <span class="text-2xl">🔑</span>
          </div>
          <div class="pl-4 text-left">
            <div class="text-xs text-gray-500 uppercase tracking-wider mb-1">Key Feature</div>
            <div class="text-lg text-slate-800 font-medium">
              Flexibility to <span class="text-transparent bg-clip-text bg-gradient-to-r from-blue-600 to-purple-600 font-bold">Swap AI Models</span> & Agentic Frameworks & New Tech/ERP Upgrades
            </div>
          </div>
        </div>
      </div>

    </div>

  </div>
</template>
