---
theme: seriph
background: https://source.unsplash.com/collection/94734566/1920x1080
class: 'text-center'
highlighter: shiki
lineNumbers: false
info: |
  ## Fantasy World Toys
  Pitch Presentation
drawings:
  persist: false
transition: slide-left

title: Fantasy World Toys Logistics
---

# Hi.

<div class="abs-br m-6 flex gap-2">
  <a href="https://github.com/rv/fwt-slidev" target="_blank" alt="GitHub"
    class="text-xl slidev-icon-btn opacity-50 !border-none !hover:text-white">
    <carbon-logo-github />
  </a>
</div>

<!--
The vision is to head towards Super Express delivery that is less than one hour.
-->

---



<SlideProfile
  name="Raghuveer (RV)"
  photoUrl="/rv_profile.jpg"
  punchlineHTML='AI Generalist with specific expertise in <span class="font-bold text-blue-600 dark:text-blue-400">Product</span> and <span class="font-bold text-teal-600 dark:text-teal-400">Communication</span>'
  context="Responsible for product, UX, prototyping, business logic and communication."
  :expertise="['Startups', 'Marketplace Businesses', 'Applied AI']"
  :pastWork="[
    { label: 'Nas Daily', bg: '#FECC00', color: 'black' },
    { label: 'Uber', bg: 'black', color: 'white' },
    { label: 'ofo', bg: '#ffe600', color: 'black' },
    { label: 'Red.Health', bg: '#D93025', color: 'white' }
  ]"
/>

---

<SlideProfile
  name="Dr. Akshay Zadgaonkar"
  photoUrl="/akshay_profile.jpg"
  punchlineHTML='AI Engineer before the AI hype.<br>25+ years in tech.'
  context="Responsible for system design, ETL, data analysis, code and AI Model training"
  :expertise="['ERP', 'Core AI']"
  :pastWork="[
    { label: 'Microsoft', bg: '#F25022', color: 'white' },
    { label: 'UNDP', bg: '#004DB1', color: 'white' },
    { label: 'Alcobev ERP', bg: '#000000', color: 'white' },
    { label: 'MS Heatwave', bg: '#7FBA00', color: 'white' }
  ]"
/>



---

<SlideHowWeWork />

---

<SlideBigBet />

---
layout: center
class: text-white bg-gradient-to-br from-slate-900 via-slate-800 to-slate-900
---

# For Fantasy World Toys

---
layout: none
---

<div class="absolute inset-0 w-full h-full bg-gradient-to-br from-slate-900 via-slate-800 to-slate-900">
  <SlideWorkSoFar />
</div>

---
layout: center
---

# The Final Scope

<div class="grid grid-cols-3 gap-8 mt-10">
  <div v-click class="flex flex-col items-center justify-center p-6 rounded-full bg-blue-500/20 hover:bg-blue-500/40 transition duration-300 cursor-pointer w-60 h-60 border-2 border-blue-400" @click="$slidev.nav.go(6)">
    <div class="text-4xl mb-2">🧠</div>
    <div class="text-xl font-bold">Project<br>EDison</div>
    <div class="text-sm opacity-70 mt-2">Decision Engine</div>
    <a href="https://docs.google.com/document/d/19Dl1Az9h-1jPL8y7-ZxjJ9wYXtniJbVb/edit?usp=sharing&ouid=100238475620801699495&rtpof=true&sd=true" target="_blank" @click.stop class="mt-3 text-xs bg-white/20 px-3 py-1 rounded-full hover:bg-white/40 transition inline-block text-gray-600 no-underline">
      📄 Full Brief
    </a>
  </div>

  <div v-click class="flex flex-col items-center justify-center p-6 rounded-full bg-green-500/20 hover:bg-green-500/40 transition duration-300 cursor-pointer w-60 h-60 border-2 border-green-400" @click="$slidev.nav.go(7)">
    <div class="text-4xl mb-2">🦅</div>
    <div class="text-xl font-bold">Project<br>Eagle</div>
    <div class="text-sm opacity-70 mt-2">Admin Platform</div>
    <a href="https://docs.google.com/document/d/1VFjBW3YeVFN6_qxiByxgZPQ-DIsd6012/edit" target="_blank" @click.stop class="mt-3 text-xs bg-white/20 px-3 py-1 rounded-full hover:bg-white/40 transition inline-block text-gray-600 no-underline">
      📄 Full Brief
    </a>
  </div>

  <div v-click class="flex flex-col items-center justify-center p-6 rounded-full bg-red-500/20 hover:bg-red-500/40 transition duration-300 cursor-pointer w-60 h-60 border-2 border-red-400" @click="$slidev.nav.go(8)">
    <div class="text-4xl mb-2">🏎️</div>
    <div class="text-xl font-bold">Project<br>HotWheels</div>
    <div class="text-sm opacity-70 mt-2">Driver App</div>
    <a href="https://docs.google.com/document/d/15y3uhWY9_0-tW4kUzxMX_LYkCedZqd40/edit" target="_blank" @click.stop class="mt-3 text-xs bg-white/20 px-3 py-1 rounded-full hover:bg-white/40 transition inline-block text-gray-600 no-underline">
      📄 Full Brief
    </a>
  </div>
</div>

<!--
Three major components working in harmony.
-->

---
transition: fade-out
---

# Project EDison
<div class="opacity-50">The Intelligent Decision Making System</div>

<div class="grid grid-cols-2 gap-8 mt-8">
  <div class="prose">
    <ul>
      <li v-click><b>AI-Driven Order Routing</b><br>
        <span class="text-sm opacity-70">Inventory + Distance + Capacity scoring</span>
      </li>
      <li v-click><b>Optimization Core</b><br>
        <span class="text-sm opacity-70">Orchestrated via n8n on Azure</span>
      </li>
      <li v-click><b>Super Express Priority</b><br>
        <span class="text-sm opacity-70">Logic to prioritize <1h deliveries</span>
      </li>
      <li v-click><b>Smart Fulfillment</b><br>
        <span class="text-sm opacity-70">Splitting orders across warehouses/stores</span>
      </li>
    </ul>
  </div>
  <div class="flex items-center justify-center">
    <!-- Placeholder for Architecture Diagram if needed -->
    <div class="text-9xl">🧠</div>
  </div>
</div>

---
transition: fade-out
---

# Project Eagle
<div class="opacity-50">Delivery Admin & Analytics Platform</div>

<div class="grid grid-cols-2 gap-8 mt-8">
  <div class="flex items-center justify-center">
    <div class="text-9xl">🦅</div>
  </div>
  <div class="prose">
    <ul>
      <li v-click><b>Control Tower</b><br>
        <span class="text-sm opacity-70">Centralized view for dispatchers</span>
      </li>
      <li v-click><b>Real-Time Tracking</b><br>
        <span class="text-sm opacity-70">Live map of all 10+ drivers</span>
      </li>
      <li v-click><b>Auto-Allocation</b><br>
        <span class="text-sm opacity-70">Nearest Available vs. Round Robin</span>
      </li>
      <li v-click><b>Validation</b><br>
        <span class="text-sm opacity-70">Proof of Delivery (POD) verification</span>
      </li>
    </ul>
  </div>
</div>

---
transition: fade-out
---

# Project HotWheels
<div class="opacity-50">Driver Mobile Application</div>

<div class="grid grid-cols-2 gap-8 mt-8">
  <div class="prose">
    <ul>
      <li v-click><b>Cross-Platform</b><br>
        <span class="text-sm opacity-70">Flutter (iOS & Android)</span>
      </li>
      <li v-click><b>Seamless Execution</b><br>
        <span class="text-sm opacity-70">Micro-task workflow (Pickup -> Dropoff)</span>
      </li>
      <li v-click><b>Resilience</b><br>
        <span class="text-sm opacity-70">Offline capabilities & data sync</span>
      </li>
      <li v-click><b>Proof</b><br>
        <span class="text-sm opacity-70">Photo capture with EXIF validation</span>
      </li>
    </ul>
  </div>
  <div class="flex items-center justify-center">
    <div class="text-9xl">🏎️</div>
  </div>
</div>

---
layout: center
class: text-white bg-gradient-to-br from-slate-900 via-slate-800 to-slate-900
---

# Solution Landscape

---

# Tech Stack

<div class="grid grid-cols-3 gap-6 mt-10 text-center">
  <div v-click class="p-4 bg-gray-100 dark:bg-gray-800 rounded-lg">
    <div class="text-2xl font-bold mb-2">Core</div>
    <div class="text-sm">Dynamics AX 2012</div>
    <div class="text-sm">Magento</div>
  </div>
  
  <div v-click class="p-4 bg-gray-100 dark:bg-gray-800 rounded-lg">
    <div class="text-2xl font-bold mb-2">API & Auth</div>
    <div class="text-sm">.NET Wrapper APIs</div>
    <div class="text-sm">JWT Auth</div>
  </div>

  <div v-click class="p-4 bg-gray-100 dark:bg-gray-800 rounded-lg">
    <div class="text-2xl font-bold mb-2">Client</div>
    <div class="text-sm">Flutter (Mobile)</div>
    <div class="text-sm">Vue/React (Admin)</div>
  </div>

  <div v-click class="p-4 bg-gray-100 dark:bg-gray-800 rounded-lg">
    <div class="text-2xl font-bold mb-2">Location</div>
    <div class="text-sm">Google Maps API</div>
    <div class="text-sm">Places API</div>
  </div>

  <div v-click class="p-4 bg-gray-100 dark:bg-gray-800 rounded-lg">
    <div class="text-2xl font-bold mb-2">Communication</div>
    <div class="text-sm">WhatsApp API</div>
    <div class="text-sm">Octopus API</div>
    <div class="text-sm">GetStream.io (or alternative)</div>
  </div>

   <div v-click class="p-4 bg-gray-100 dark:bg-gray-800 rounded-lg">
    <div class="text-2xl font-bold mb-2">Infra</div>
    <div class="text-sm">Azure</div>
    <div class="text-sm">n8n</div>
  </div>

  <div v-click class="p-4 bg-gray-100 dark:bg-gray-800 rounded-lg">
    <div class="text-2xl font-bold mb-2">Database</div>
    <div class="text-sm">PostgreSQL</div>
  </div>
</div>


---
layout: none
clicks: 17
---

<div class="w-full h-full bg-gradient-to-br from-slate-900 via-slate-800 to-slate-900">
  <StaticArchitectureDiagram />
</div>

<!--
Step-by-step breakdown of the solution landscape.
-->

---
layout: none
---

<div class="w-full h-full bg-gradient-to-br from-slate-900 via-slate-800 to-slate-900">
  <AnimatedArchitectureDiagram />
</div>

<!--
This shows the complete end-to-end architecture with all components working together.
The animated flow demonstrates how data moves through the system in real-time.
-->

---

# Delivery Timeline

<div class="w-full mt-4">

```mermaid
gantt
    %%{init: {'theme': 'base', 'themeVariables': { 'fontSize': '24px', 'fontFamily': 'serif'}, 'gantt': {'barHeight': 90, 'sectionFontSize': '28', 'fontSize': '24', 'topPadding': 25, 'bottomPadding': 25, 'leftPadding': 220} } }%%
    dateFormat YYYY-MM-DD
    axisFormat %b
    tickInterval 1month
    section Kick off
    Kuwait Visit & Immersion    :k1, 2025-01-01, 5d
    section System design
    Architecture & APIs         :s1, after k1, 7d
    section Product design
    UI/UX Design & Prototypes   :p1, after k1, 10d
    section Development
    All 3 Projects (90 Days)    :d1, after s1, 90d
    section Deployment
    Infrastructure Setup        :dep1, after d1, 7d
    section Maintenance
    Ongoing Support & Updates   :m1, after dep1, 30d
    section Launch
    UAT & Training              :l1, after d1, 10d
    section Support
    Go-Live Support             :sup1, after l1, 20d
```

</div>

---

# Project-wise Execution Map

<div class="w-full mt-4">

```mermaid
gantt
    %%{init: {'theme': 'base', 'themeVariables': { 'fontSize': '24px', 'fontFamily': 'serif'}, 'gantt': {'barHeight': 90, 'sectionFontSize': '28', 'fontSize': '24', 'topPadding': 25, 'bottomPadding': 25, 'leftPadding': 220} } }%%
    dateFormat  YYYY-MM-DD
    axisFormat  %b
    tickInterval 1month

    section Edison
    Core Logic & Inference  :active, e1, 2025-01-01, 30d

    section Eagle
    Admin & Control Tower   :des1, 2025-01-21, 90d

    section HotWheels
    App Development         :des2, 2025-01-21, 90d

    section Edison​
    Model Refinement        :active, e2, 2025-04-01, 30d
```

</div>

---
layout: center
---

# The Team

<div class="flex justify-center gap-12 mt-10">
  <div class="text-center">
    <div class="w-32 h-32 bg-gray-300 rounded-full mx-auto mb-4 flex items-center justify-center text-4xl">👨‍💻</div>
    <div class="font-bold text-xl">RV</div>
    <div class="text-sm opacity-70">Lead</div>
  </div>

  <div class="text-center">
    <div class="w-32 h-32 bg-gray-300 rounded-full mx-auto mb-4 flex items-center justify-center text-4xl">🔬</div>
    <div class="font-bold text-xl">Dr. Akshay Zadgaonkar</div>
    <div class="text-sm opacity-70">Expert</div>
  </div>

  <div class="text-center">
    <div class="w-32 h-32 bg-gray-300 rounded-full mx-auto mb-4 flex items-center justify-center text-4xl">🚀</div>
    <div class="font-bold text-xl">Flash</div>
    <div class="text-sm opacity-70">Development</div>
  </div>
</div>

---

# Commercial Proposal

<div class="mt-10">
  <table class="w-full text-left border-collapse">
    <thead>
      <tr class="border-b border-gray-400">
        <th class="py-2 text-xl">Item / Activity</th>
        <th class="py-2 text-xl text-right">Cost (KD)</th>
      </tr>
    </thead>
    <tbody>
      <tr class="border-b border-gray-200 dark:border-gray-700">
        <td class="py-4">
          <div class="font-bold text-lg">System & Product Design</div>
          <div class="text-sm opacity-70">Includes 3-4 day on-site visit (Kick-off, Immersion, Interviews)</div>
        </td>
        <td class="py-4 text-right font-mono text-lg">9,600</td>
      </tr>
      <tr class="border-b border-gray-200 dark:border-gray-700">
        <td class="py-4">
          <div class="font-bold text-lg">Development</div>
          <div class="text-sm opacity-70">ETL, n8n, Postgres, API, AI Models, Frontend</div>
        </td>
        <td class="py-4 text-right font-mono text-lg">5,000</td>
      </tr>
      <tr class="border-b border-gray-200 dark:border-gray-700">
        <td class="py-4">
          <div class="font-bold text-lg">Deployment</div>
          <div class="text-sm opacity-70">Infrastructure setup, Cloud configuration</div>
        </td>
        <td class="py-4 text-right font-mono text-lg">1,400</td>
      </tr>
      <tr class="border-b border-gray-200 dark:border-gray-700">
        <td class="py-4">
          <div class="font-bold text-lg">Maintenance</div>
          <div class="text-sm opacity-70">Support & Updates</div>
        </td>
        <td class="py-4 text-right font-mono text-lg">1,200</td>
      </tr>
      <tr class="font-bold text-xl bg-blue-500/10">
        <td class="py-4 pl-4 rounded-l-lg">Total Investment</td>
        <td class="py-4 pr-4 text-right rounded-r-lg">17,200 KD</td>
      </tr>
    </tbody>
  </table>
</div>

---
layout: center
class: text-white bg-gradient-to-br from-slate-900 via-slate-800 to-slate-900
---

# Annexure

---

# Scope Evolution
<div class="opacity-50 text-sm">From Data Analysis to Complete Delivery Platform</div>

<div class="grid grid-cols-2 gap-6 mt-3">
  <div class="p-4 bg-gray-100 dark:bg-gray-800 rounded-lg">
    <div class="text-xl font-bold mb-2 text-blue-500">Original Scope</div>
    <div class="text-xs opacity-70 mb-2">3 months timeline</div>
    <div class="text-sm space-y-1 mt-2">
      <div>✓ Project EDison only</div>
      <div>✓ Data analysis & reporting from AX 2012</div>
      <div>✓ Delivery intelligence insights</div>
      <div>✓ Warehouse dispatch suggestions</div>
      <div>✓ Inventory stocking recommendations</div>
      <div>✓ 2-person team</div>
    </div>
    <div class="mt-3 p-3 bg-blue-500/20 rounded-lg">
      <div class="text-xs opacity-70">Investment</div>
      <div class="text-2xl font-bold">6,000 KD</div>
    </div>
  </div>

  <div class="p-4 bg-gradient-to-br from-green-500/20 to-blue-500/20 rounded-lg border-2 border-green-400">
    <div class="text-xl font-bold mb-2 text-green-500">Enhanced Scope</div>
    <div class="text-xs opacity-70 mb-2">4 months timeline + 12 months support</div>
    <div class="text-sm space-y-1 mt-2">
      <div><b>🧠 EDison:</b> Enhanced AI decision engine</div>
      <div><b>🦅 Eagle:</b> Complete control tower web app</div>
      <div><b>🏎️ HotWheels:</b> Cross-platform driver app</div>
      <div>• 50+ screens designed & developed</div>
      <div>• Real-time tracking & dispatch</div>
      <div>• Offline-capable mobile apps</div>
      <div>• 5-person team (Senior Frontend, Backend, Testing)</div>
      <div>• 12 months ongoing support</div>
      <div>• OS updates & security patches</div>
    </div>
    <div class="mt-3 p-3 bg-green-500/30 rounded-lg">
      <div class="text-xs opacity-70">Investment</div>
      <div class="text-2xl font-bold">17,200 KD</div>
      <div class="text-xs opacity-70 mt-1">2.87x value for complete platform</div>
    </div>
  </div>
</div>

---
layout: center
class: text-center
---

# Exclusions

<div class="text-left inline-block mt-8">
  <ul class="text-xl">
    <li class="mb-4">🚫 Third-party subscription costs</li>
    <li>🚫 API usage costs (Google Maps, etc.)</li>
  </ul>
</div>

---
layout: center
class: text-center
---

# Exclusions & Future Opportunities
<div class="opacity-50">Scope Boundaries</div>

<div class="text-left inline-block mt-8">
  <ul class="text-lg">
    <li class="mb-3">🚫 Customer-facing application features</li>
    <li class="mb-3">🚫 Driver payroll and compensation management</li>
    <li class="mb-3">🚫 Direct AX 2012 API development (FWT in-house responsibility)</li>
    <li class="mb-3">🚫 Direct Magento webhook development (FWT in-house responsibility)</li>
    <li class="mb-3">🚫 Task rejection by driver (all assigned tasks must be attempted)</li>
    <li class="mb-3">🚫 Vehicle maintenance tracking</li>
    <li>🚫 Fuel tracking or reimbursement</li>
  </ul>
</div>

---
layout: center
class: text-center
---

# Project Eagle Demo 🦅

<div class="mt-16">
  <a href="http://localhost:5173/login" target="_blank" class="inline-block px-12 py-6 bg-green-500 hover:bg-green-600 text-white text-2xl font-bold rounded-lg transition duration-300 no-underline shadow-lg hover:shadow-xl">
    Launch Demo
  </a>
</div>

<div class="mt-8 text-sm opacity-70">
  Click to open the Project Eagle admin platform
</div>

---
layout: end
---

# Thank You

Fantasy World Toys × RV
