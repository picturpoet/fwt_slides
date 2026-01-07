<script setup lang="ts">
import { ref, onMounted, onUnmounted, computed } from 'vue'

const isPlaying = ref(true)
const currentStep = ref(0)
const showLabels = ref(true)
let interval: NodeJS.Timeout | null = null

const steps = [
  { id: 0, label: 'Order Placed', description: 'Customer order → AX' },
  { id: 1, label: 'ETL Extract', description: 'Data pulled from AX' },
  { id: 2, label: 'Processing', description: 'PostgreSQL + Services' },
  { id: 3, label: 'AI Analysis', description: 'Edison optimizes route' },
  { id: 4, label: 'Dispatch', description: 'Driver assigned via Eagle' },
  { id: 5, label: 'Driver App', description: 'Hot Wheels notification' },
  { id: 6, label: 'Customer Alert', description: 'WhatsApp/SMS update' },
  { id: 7, label: 'Status Update', description: 'Back to AX' },
]

const currentStepLabel = computed(() => steps[currentStep.value].label)
const currentStepDesc = computed(() => steps[currentStep.value].description)

onMounted(() => {
  startAnimation()
})

onUnmounted(() => {
  stopAnimation()
})

const startAnimation = () => {
  interval = setInterval(() => {
    currentStep.value = (currentStep.value + 1) % steps.length
  }, 2500)
}

const stopAnimation = () => {
  if (interval) {
    clearInterval(interval)
    interval = null
  }
}

const togglePlay = () => {
  isPlaying.value = !isPlaying.value
  if (isPlaying.value) {
    startAnimation()
  } else {
    stopAnimation()
  }
}

const toggleLabels = () => {
  showLabels.value = !showLabels.value
}
</script>

<template>
  <div class="relative w-full h-full bg-transparent text-white overflow-hidden">
    
    <!-- Main Diagram SVG - ViewBox 1250x650 -->
    <svg viewBox="0 0 1280 720" class="w-full h-full block">
      <defs>
        <!-- Gradients -->
        <linearGradient id="anim-grad-bg" x1="0%" y1="0%" x2="100%" y2="100%">
          <stop offset="0%" stop-color="#1E293B" />
          <stop offset="100%" stop-color="#0F172A" />
        </linearGradient>
        <linearGradient id="anim-grad-box" x1="0%" y1="0%" x2="0%" y2="100%">
          <stop offset="0%" stop-color="#334155" />
          <stop offset="100%" stop-color="#1E293B" />
        </linearGradient>
        
        <!-- Glow effect -->
        <filter id="anim-glow" x="-50%" y="-50%" width="200%" height="200%">
          <feGaussianBlur stdDeviation="3" result="coloredBlur"/>
          <feMerge>
            <feMergeNode in="coloredBlur"/>
            <feMergeNode in="SourceGraphic"/>
          </feMerge>
        </filter>
        
        <!-- Strong glow for active elements -->
        <filter id="anim-glow-strong" x="-100%" y="-100%" width="300%" height="300%">
          <feGaussianBlur stdDeviation="6" result="coloredBlur"/>
          <feMerge>
            <feMergeNode in="coloredBlur"/>
            <feMergeNode in="coloredBlur"/>
            <feMergeNode in="SourceGraphic"/>
          </feMerge>
        </filter>
      </defs>

      <!-- Background -->
      <rect width="1280" height="720" fill="url(#anim-grad-bg)" />
      
      <!-- Grid pattern -->
      <pattern id="anim-grid" width="30" height="30" patternUnits="userSpaceOnUse">
        <path d="M 30 0 L 0 0 0 30" fill="none" stroke="rgba(148,163,184,0.05)" stroke-width="1"/>
      </pattern>
      <rect width="1280" height="720" fill="url(#anim-grid)" />

      <!-- ========== STATUS BAR (Header) ========== -->
      <g transform="translate(325, 30)">
        <rect x="0" y="0" width="600" height="30" rx="15" fill="rgba(30, 41, 59, 0.8)" stroke="#475569" stroke-width="1" />
        <g transform="translate(15, 15)">
          <circle v-for="(step, i) in steps" :key="i" :cx="i * 15" cy="0" r="4" 
            :fill="i === currentStep ? '#22C55E' : (i < currentStep ? '#22C55E' : '#475569')" 
            :opacity="i < currentStep ? 0.5 : 1"
          />
        </g>
        <text x="140" y="15" font-size="6" fill="#4ADE80" font-weight="bold" dominant-baseline="middle">
          Step {{ currentStep + 1 }}: {{ currentStepLabel }}
        </text>
      </g>

      <!-- ========== LAYER LABELS (Bottom) ========== -->
      <g v-if="showLabels">
        <rect x="20" y="80" width="160" height="40" rx="8" fill="rgba(124, 58, 237, 0.15)" stroke="#7C3AED" stroke-width="1" stroke-dasharray="4,2" />
        <text x="100" y="100" font-size="5" fill="#A78BFA" text-anchor="middle" dominant-baseline="middle" font-weight="bold">ERP LAYER</text>
        
        <rect x="900" y="80" width="180" height="40" rx="8" fill="rgba(59, 130, 246, 0.15)" stroke="#3B82F6" stroke-width="1" stroke-dasharray="4,2" />
        <text x="990" y="100" font-size="5" fill="#60A5FA" text-anchor="middle" dominant-baseline="middle" font-weight="bold">FRONTEND APPS</text>
        
        <rect x="1110" y="80" width="100" height="40" rx="8" fill="rgba(16, 185, 129, 0.15)" stroke="#10B981" stroke-width="1" stroke-dasharray="4,2" />
        <text x="1160" y="100" font-size="5" fill="#34D399" text-anchor="middle" dominant-baseline="middle" font-weight="bold">COMMS</text>
      </g>

      <!-- ========== DEVELOPMENT SCOPE BOUNDARY ========== -->
      <rect x="260" y="80" width="620" height="560" rx="16" fill="rgba(236, 72, 153, 0.05)" stroke="#EC4899" stroke-width="2" stroke-dasharray="10,5" />
      <rect x="260" y="80" width="620" height="35" rx="16" fill="rgba(236, 72, 153, 0.15)" />
      <text x="570" y="104" font-size="5" fill="#F472B6" text-anchor="middle" font-weight="bold">
        📦 DEVELOPMENT SCOPE — RV &amp; Akshay Team
      </text>

      <!-- ========== COMPONENTS ========== -->
      
      <!-- AX 2012 -->
      <g :filter="(currentStep === 0 || currentStep === 7) ? 'url(#anim-glow-strong)' : ''">
        <rect x="25" y="140" width="160" height="200" rx="10" fill="url(#anim-grad-box)" stroke="#7C3AED" stroke-width="2" />
        <rect x="25" y="140" width="160" height="32" rx="10" fill="#7C3AED" />
        <text x="35" y="162" font-size="4.5">🏢</text>
        <text x="55" y="162" font-size="4.5" fill="white" font-weight="bold">Dynamics AX</text>
        <text x="43" y="190" font-size="3.5" fill="#E2E8F0">• Sales Orders</text>
        <text x="43" y="210" font-size="3.5" fill="#E2E8F0">• Inventory Data</text>
        <text x="43" y="230" font-size="3.5" fill="#E2E8F0">• Customer Info</text>
        <text x="43" y="250" font-size="3.5" fill="#E2E8F0">• Driver Roster</text>
        <text x="43" y="270" font-size="3.5" fill="#E2E8F0">• Trip Scheduler</text>
        <!-- LIVE Badge -->
        <rect x="138" y="315" width="36" height="14" rx="7" fill="#22C55E" />
        <text x="155" y="322" font-size="3" fill="white" text-anchor="middle" dominant-baseline="middle" font-weight="bold">LIVE</text>
        
        <!-- Pulsing Ring -->
        <g v-if="currentStep === 0 || currentStep === 7" style="transition: opacity 0.5s">
          <circle cx="105" cy="240" r="20" fill="none" stroke="#7C3AED" stroke-width="3">
            <animate attributeName="r" values="20;35;20" dur="1.5s" repeatCount="indefinite" />
            <animate attributeName="opacity" values="1;0;1" dur="1.5s" repeatCount="indefinite" />
          </circle>
        </g>
      </g>

      <!-- Future ERP -->
      <g opacity="0.4">
        <rect x="25" y="380" width="160" height="60" rx="10" fill="transparent" stroke="#A78BFA" stroke-width="1" stroke-dasharray="6,3" />
        <text x="105" y="408" font-size="4" fill="#A78BFA" text-anchor="middle">Future ERP</text>
        <text x="105" y="425" font-size="3" fill="#A78BFA" text-anchor="middle">(Upgrade Ready)</text>
      </g>

      <!-- ETL Services -->
      <g :filter="currentStep === 1 ? 'url(#anim-glow-strong)' : ''">
        <rect x="280" y="190" width="120" height="100" rx="10" fill="url(#anim-grad-box)" stroke="#6366F1" stroke-width="2" />
        <rect x="280" y="190" width="120" height="28" rx="10" fill="#6366F1" />
        <text x="290" y="210" font-size="4.5">⚙️</text>
        <text x="310" y="210" font-size="4.5" fill="white" font-weight="bold">ETL</text>
        <!-- .NET Tag (tight width) -->
        <rect x="362" y="274" width="32" height="12" rx="6" fill="rgba(255,255,255,0.2)" />
        <text x="378" y="282" font-size="2.5" fill="white" text-anchor="middle" dominant-baseline="middle">.NET</text>
        <text x="295" y="235" font-size="3.5" fill="#E2E8F0">• Data Extraction</text>
        <text x="295" y="252" font-size="3.5" fill="#E2E8F0">• Transform</text>
        <text x="295" y="269" font-size="3.5" fill="#E2E8F0">• Load to DB</text>
        <!-- Pulsing Ring -->
        <g v-if="currentStep === 1" style="transition: opacity 0.5s">
          <circle cx="340" cy="240" r="20" fill="none" stroke="#6366F1" stroke-width="3">
            <animate attributeName="r" values="20;35;20" dur="1.5s" repeatCount="indefinite" />
            <animate attributeName="opacity" values="1;0;1" dur="1.5s" repeatCount="indefinite" />
          </circle>
        </g>
      </g>

      <!-- n8n Workflows -->
      <g :filter="currentStep === 1 ? 'url(#anim-glow-strong)' : ''">
        <rect x="280" y="310" width="120" height="85" rx="10" fill="url(#anim-grad-box)" stroke="#F97316" stroke-width="2" />
        <rect x="280" y="310" width="120" height="28" rx="10" fill="#F97316" />
        <text x="290" y="330" font-size="4.5">🔄</text>
        <text x="310" y="330" font-size="4.5" fill="white" font-weight="bold">n8n</text>
        <text x="295" y="358" font-size="3.5" fill="#E2E8F0">• No-Code Logic</text>
        <text x="295" y="375" font-size="3.5" fill="#E2E8F0">• Orchestration</text>
      </g>

      <!-- PostgreSQL -->
      <g :filter="currentStep === 2 ? 'url(#anim-glow-strong)' : ''">
        <rect x="460" y="240" width="150" height="130" rx="10" fill="url(#anim-grad-box)" stroke="#0EA5E9" stroke-width="2" />
        <rect x="460" y="240" width="150" height="28" rx="10" fill="#0EA5E9" />
        <text x="470" y="260" font-size="4.5">🗄️</text>
        <text x="490" y="260" font-size="4.5" fill="white" font-weight="bold">PostgreSQL</text>
        <!-- DB Tag (tight width) -->
        <rect x="579" y="354" width="20" height="12" rx="6" fill="rgba(255,255,255,0.2)" />
        <text x="589" y="362" font-size="2.5" fill="white" text-anchor="middle" dominant-baseline="middle">DB</text>
        <text x="475" y="288" font-size="3.5" fill="#E2E8F0">• Central Database</text>
        <text x="475" y="305" font-size="3.5" fill="#E2E8F0">• Order States</text>
        <text x="475" y="322" font-size="3.5" fill="#E2E8F0">• Driver Data</text>
        <text x="475" y="339" font-size="3.5" fill="#E2E8F0">• Analytics Store</text>
        <!-- Pulsing Ring -->
        <g v-if="currentStep === 2" style="transition: opacity 0.5s">
          <circle cx="535" cy="305" r="20" fill="none" stroke="#0EA5E9" stroke-width="3">
            <animate attributeName="r" values="20;35;20" dur="1.5s" repeatCount="indefinite" />
            <animate attributeName="opacity" values="1;0;1" dur="1.5s" repeatCount="indefinite" />
          </circle>
        </g>
      </g>

      <!-- Microservices -->
      <g :filter="currentStep === 2 ? 'url(#anim-glow-strong)' : ''">
        <rect x="460" y="420" width="150" height="100" rx="10" fill="url(#anim-grad-box)" stroke="#8B5CF6" stroke-width="2" />
        <rect x="460" y="420" width="150" height="28" rx="10" fill="#8B5CF6" />
        <text x="470" y="440" font-size="4.5">🔧</text>
        <text x="490" y="440" font-size="4.5" fill="white" font-weight="bold">Microservices</text>
        <!-- .NET Tag (tight width) -->
        <rect x="574" y="504" width="32" height="12" rx="6" fill="rgba(255,255,255,0.2)" />
        <text x="590" y="512" font-size="2.5" fill="white" text-anchor="middle" dominant-baseline="middle">.NET</text>
        <text x="475" y="468" font-size="3.5" fill="#E2E8F0">• Business Logic</text>
        <text x="475" y="485" font-size="3.5" fill="#E2E8F0">• API Gateway</text>
        <text x="475" y="502" font-size="3.5" fill="#E2E8F0">• State Mgmt</text>
      </g>

      <!-- FastAPI -->
      <g :filter="currentStep === 3 ? 'url(#anim-glow-strong)' : ''">
        <rect x="680" y="240" width="140" height="100" rx="10" fill="url(#anim-grad-box)" stroke="#10B981" stroke-width="2" />
        <rect x="680" y="240" width="140" height="28" rx="10" fill="#10B981" />
        <text x="690" y="260" font-size="4.5">⚡</text>
        <text x="710" y="260" font-size="4.5" fill="white" font-weight="bold">FastAPI</text>
        <!-- PYTHON Tag (tight width) -->
        <rect x="775" y="324" width="42" height="12" rx="6" fill="rgba(255,255,255,0.2)" />
        <text x="796" y="332" font-size="2.5" fill="white" text-anchor="middle" dominant-baseline="middle">PYTHON</text>
        <text x="695" y="288" font-size="3.5" fill="#E2E8F0">• REST APIs</text>
        <text x="695" y="305" font-size="3.5" fill="#E2E8F0">• AI Inference</text>
        <text x="695" y="322" font-size="3.5" fill="#E2E8F0">• Real-time</text>
      </g>

      <!-- AI Models -->
      <g :filter="currentStep === 3 ? 'url(#anim-glow-strong)' : ''">
        <rect x="680" y="360" width="140" height="130" rx="10" fill="url(#anim-grad-box)" stroke="#F59E0B" stroke-width="2" />
        <rect x="680" y="360" width="140" height="28" rx="10" fill="#F59E0B" />
        <text x="690" y="380" font-size="4.5">🧠</text>
        <text x="710" y="380" font-size="4.5" fill="white" font-weight="bold">AI Models</text>

        <text x="695" y="410" font-size="3.5" fill="#E2E8F0">• Route Optimization</text>
        <text x="695" y="427" font-size="3.5" fill="#E2E8F0">• Smart Allocation</text>
        <text x="695" y="444" font-size="3.5" fill="#E2E8F0">• Predictions</text>
        <text x="695" y="461" font-size="3.5" fill="#E2E8F0">• Training Pipeline</text>
        <!-- Pulsing Ring -->
        <g v-if="currentStep === 3" style="transition: opacity 0.5s">
          <circle cx="750" cy="425" r="20" fill="none" stroke="#F59E0B" stroke-width="3">
            <animate attributeName="r" values="20;35;20" dur="1.5s" repeatCount="indefinite" />
            <animate attributeName="opacity" values="1;0;1" dur="1.5s" repeatCount="indefinite" />
          </circle>
        </g>
      </g>

      <!-- Edison Badge -->
      <rect x="707.5" y="495" width="85" height="22" rx="11" fill="#F59E0B" />
      <text x="750" y="506" font-size="3.5" fill="white" text-anchor="middle" dominant-baseline="middle" font-weight="bold">💡 EDISON</text>

      <!-- Training / Testing -->
      <g>
        <rect x="460" y="550" width="150" height="70" rx="10" fill="url(#anim-grad-box)" stroke="#EC4899" stroke-width="2" />
        <rect x="460" y="550" width="150" height="28" rx="10" fill="#EC4899" />
        <text x="470" y="570" font-size="4.5">🔬</text>
        <text x="490" y="570" font-size="4.5" fill="white" font-weight="bold">Training</text>
        <text x="475" y="598" font-size="3.5" fill="#E2E8F0">• Model Training</text>
        <text x="475" y="615" font-size="3.5" fill="#E2E8F0">• Validation</text>
      </g>

      <!-- Driver App -->
      <g :filter="currentStep === 5 ? 'url(#anim-glow-strong)' : ''">
        <rect x="900" y="150" width="180" height="140" rx="10" fill="url(#anim-grad-box)" stroke="#3B82F6" stroke-width="2" />
        <rect x="900" y="150" width="180" height="28" rx="10" fill="#3B82F6" />
        <text x="910" y="170" font-size="4.5">📱</text>
        <text x="930" y="170" font-size="4.5" fill="white" font-weight="bold">Driver App</text>
        <!-- FLUTTER Tag (tight width) -->
        <rect x="1026" y="274" width="48" height="14" rx="6" fill="rgba(255,255,255,0.2)" />
        <text x="1050" y="282" font-size="2.5" fill="white" text-anchor="middle" dominant-baseline="middle">FLUTTER</text>
        <text x="915" y="198" font-size="3.5" fill="#E2E8F0">• iOS + Android</text>
        <text x="915" y="215" font-size="3.5" fill="#E2E8F0">• Offline Support</text>
        <text x="915" y="232" font-size="3.5" fill="#E2E8F0">• GPS Tracking</text>
        <text x="915" y="249" font-size="3.5" fill="#E2E8F0">• POD Capture</text>
        <text x="915" y="266" font-size="3.5" fill="#E2E8F0">• Chat</text>
        <!-- Pulsing Ring -->
        <g v-if="currentStep === 5" style="transition: opacity 0.5s">
          <circle cx="980" cy="220" r="20" fill="none" stroke="#3B82F6" stroke-width="3">
            <animate attributeName="r" values="20;35;20" dur="1.5s" repeatCount="indefinite" />
            <animate attributeName="opacity" values="1;0;1" dur="1.5s" repeatCount="indefinite" />
          </circle>
        </g>
      </g>
      
      <!-- Hot Wheels Badge -->
      <rect x="940" y="295" width="120" height="22" rx="11" fill="#EF4444" />
      <text x="1000" y="306" font-size="3.5" fill="white" text-anchor="middle" dominant-baseline="middle" font-weight="bold">🚗 HOT WHEELS</text>

      <!-- Analytics Portal -->
      <g :filter="currentStep === 4 ? 'url(#anim-glow-strong)' : ''">
        <rect x="900" y="340" width="180" height="120" rx="10" fill="url(#anim-grad-box)" stroke="#14B8A6" stroke-width="2" />
        <rect x="900" y="340" width="180" height="28" rx="10" fill="#14B8A6" />
        <text x="910" y="360" font-size="4.5">🖥️</text>
        <text x="930" y="360" font-size="4.5" fill="white" font-weight="bold">Analytics Portal</text>
        <!-- WEB Tag (tight width) -->
        <rect x="1041" y="444" width="28" height="12" rx="6" fill="rgba(255,255,255,0.2)" />
        <text x="1055" y="452" font-size="2.5" fill="white" text-anchor="middle" dominant-baseline="middle">WEB</text>
        <text x="915" y="388" font-size="3.5" fill="#E2E8F0">• Control Tower</text>
        <text x="915" y="405" font-size="3.5" fill="#E2E8F0">• Real-time Map</text>
        <text x="915" y="422" font-size="3.5" fill="#E2E8F0">• Dispatch Console</text>
        <text x="915" y="439" font-size="3.5" fill="#E2E8F0">• Reports</text>
        <!-- Pulsing Ring -->
        <g v-if="currentStep === 4" style="transition: opacity 0.5s">
          <circle cx="980" cy="400" r="20" fill="none" stroke="#14B8A6" stroke-width="3">
            <animate attributeName="r" values="20;35;20" dur="1.5s" repeatCount="indefinite" />
            <animate attributeName="opacity" values="1;0;1" dur="1.5s" repeatCount="indefinite" />
          </circle>
        </g>
      </g>
      
      <!-- Eagle Badge -->
      <rect x="940" y="465" width="85" height="22" rx="11" fill="#14B8A6" />
      <text x="982.5" y="476" font-size="3.5" fill="white" text-anchor="middle" dominant-baseline="middle" font-weight="bold">🦅 EAGLE</text>

      <!-- Teams API -->
      <g>
        <rect x="1110" y="150" width="120" height="70" rx="10" fill="url(#anim-grad-box)" stroke="#7C3AED" stroke-width="2" />
        <rect x="1110" y="150" width="120" height="24" rx="10" fill="#7C3AED" />
        <text x="1120" y="167" font-size="4.5">👥</text>
        <text x="1136" y="167" font-size="4.5" fill="white" font-weight="bold">Teams</text>
        <text x="1122" y="190" font-size="3.5" fill="#E2E8F0">• Status Updates</text>
        <text x="1122" y="205" font-size="3.5" fill="#E2E8F0">• ETL Triggers</text>
      </g>

      <!-- Alerts / Communication -->
      <g :filter="currentStep === 6 ? 'url(#anim-glow-strong)' : ''">
        <rect x="1110" y="240" width="120" height="120" rx="10" fill="url(#anim-grad-box)" stroke="#10B981" stroke-width="2" />
        <rect x="1110" y="240" width="120" height="20" rx="8" fill="#10B981" />
        <text x="1120" y="257" font-size="4.5">🔔</text>
        <text x="1136" y="257" font-size="4.5" fill="white" font-weight="bold">Alerts</text>
        
        <!-- WhatsApp -->
        <rect x="1135" y="275" width="26" height="22" rx="5" fill="#25D366" />
        <text x="1148" y="291" font-size="6" text-anchor="middle">💬</text>
        
        <!-- Email -->
        <rect x="1179" y="275" width="26" height="22" rx="5" fill="#EA4335" />
        <text x="1192" y="291" font-size="6" text-anchor="middle">📧</text>
        
        <!-- SMS -->
        <rect x="1157" y="310" width="26" height="22" rx="5" fill="#3B82F6" />
        <text x="1170" y="326" font-size="6" text-anchor="middle">📱</text>
        
        <!-- Pulsing Ring -->
        <g v-if="currentStep === 6" style="transition: opacity 0.5s">
          <circle cx="1170" cy="321" r="20" fill="none" stroke="#10B981" stroke-width="3">
            <animate attributeName="r" values="20;35;20" dur="1.5s" repeatCount="indefinite" />
            <animate attributeName="opacity" values="1;0;1" dur="1.5s" repeatCount="indefinite" />
          </circle>
        </g>
      </g>



      <!-- ========== PATHS (Unchanged) ========== -->
      <path d="M 155 240 L 220 240 L 220 200 L 280 200" fill="none" stroke="rgba(124, 58, 237, 0.3)" stroke-width="3" stroke-dasharray="8,4" />
      <path d="M 400 240 L 430 240 L 430 305 L 460 305" fill="none" stroke="rgba(99, 102, 241, 0.3)" stroke-width="3" stroke-dasharray="8,4" />
      <path d="M 400 350 L 430 350 L 430 305 L 460 305" fill="none" stroke="rgba(249, 115, 22, 0.3)" stroke-width="3" stroke-dasharray="8,4" />
      <path d="M 535 370 L 535 420" fill="none" stroke="rgba(14, 165, 233, 0.3)" stroke-width="3" stroke-dasharray="8,4" />
      <path d="M 610 300 L 680 300" fill="none" stroke="rgba(14, 165, 233, 0.3)" stroke-width="3" stroke-dasharray="8,4" />
      <path d="M 750 340 L 750 360" fill="none" stroke="rgba(16, 185, 129, 0.3)" stroke-width="3" stroke-dasharray="8,4" />
      <path d="M 610 470 Q 750 450 900 220" fill="none" stroke="rgba(59, 130, 246, 0.3)" stroke-width="3" stroke-dasharray="8,4" />
      <path d="M 610 490 L 750 490 L 900 400" fill="none" stroke="rgba(20, 184, 166, 0.3)" stroke-width="3" stroke-dasharray="8,4" />
      <path d="M 1060 400 L 1110 300" fill="none" stroke="rgba(16, 185, 129, 0.3)" stroke-width="3" stroke-dasharray="8,4" />
      <path d="M 900 260 Q 500 640 155 340" fill="none" stroke="rgba(16, 185, 129, 0.3)" stroke-width="3" stroke-dasharray="8,4" />
      <!-- Training to ETL Path -->
      <path d="M 535 550 Q 430 550 430 480 L 430 300 Q 430 290 340 290" fill="none" stroke="rgba(236, 72, 153, 0.4)" stroke-width="3" stroke-dasharray="8,4" />

      <!-- ========== ANIMATED FLOWING PARTICLES (Unchanged) ========== -->
      <g v-if="isPlaying">
        <g><circle v-for="i in 3" :key="'p1-'+i" r="6" fill="#A78BFA" filter="url(#anim-glow)"><animateMotion dur="2s" repeatCount="indefinite" :begin="(i-1)*2/3 + 's'" path="M 155 240 L 220 240 L 220 200 L 280 200" /><animate attributeName="opacity" values="0;1;1;0" dur="2s" repeatCount="indefinite" :begin="(i-1)*2/3 + 's'" /></circle></g>
        <g><circle v-for="i in 2" :key="'p2-'+i" r="6" fill="#818CF8" filter="url(#anim-glow)"><animateMotion dur="1.5s" repeatCount="indefinite" :begin="0.5 + (i-1)*1.5/2 + 's'" path="M 400 240 L 430 240 L 430 305 L 460 305" /><animate attributeName="opacity" values="0;1;1;0" dur="1.5s" repeatCount="indefinite" :begin="0.5 + (i-1)*1.5/2 + 's'" /></circle></g>
        <g><circle v-for="i in 2" :key="'p3-'+i" r="6" fill="#FB923C" filter="url(#anim-glow)"><animateMotion dur="1.5s" repeatCount="indefinite" :begin="1 + (i-1)*1.5/2 + 's'" path="M 400 350 L 430 350 L 430 305 L 460 305" /><animate attributeName="opacity" values="0;1;1;0" dur="1.5s" repeatCount="indefinite" :begin="1 + (i-1)*1.5/2 + 's'" /></circle></g>
        <g><circle v-for="i in 2" :key="'p4-'+i" r="6" fill="#38BDF8" filter="url(#anim-glow)"><animateMotion dur="1s" repeatCount="indefinite" :begin="1.5 + (i-1)*1/2 + 's'" path="M 535 370 L 535 420" /><animate attributeName="opacity" values="0;1;1;0" dur="1s" repeatCount="indefinite" :begin="1.5 + (i-1)*1/2 + 's'" /></circle></g>
        <g><circle v-for="i in 2" :key="'p5-'+i" r="6" fill="#38BDF8" filter="url(#anim-glow)"><animateMotion dur="1s" repeatCount="indefinite" :begin="1.5 + (i-1)*1/2 + 's'" path="M 610 300 L 680 300" /><animate attributeName="opacity" values="0;1;1;0" dur="1s" repeatCount="indefinite" :begin="1.5 + (i-1)*1/2 + 's'" /></circle></g>
        <g><circle v-for="i in 2" :key="'p6-'+i" r="6" fill="#34D399" filter="url(#anim-glow)"><animateMotion dur="1s" repeatCount="indefinite" :begin="2 + (i-1)*1/2 + 's'" path="M 750 340 L 750 360" /><animate attributeName="opacity" values="0;1;1;0" dur="1s" repeatCount="indefinite" :begin="2 + (i-1)*1/2 + 's'" /></circle></g>
        <g><circle v-for="i in 4" :key="'p7-'+i" r="6" fill="#60A5FA" filter="url(#anim-glow)"><animateMotion dur="2.5s" repeatCount="indefinite" :begin="2.5 + (i-1)*2.5/4 + 's'" path="M 610 470 Q 750 450 900 220" /><animate attributeName="opacity" values="0;1;1;0" dur="2.5s" repeatCount="indefinite" :begin="2.5 + (i-1)*2.5/4 + 's'" /></circle></g>
        <g><circle v-for="i in 3" :key="'p8-'+i" r="6" fill="#2DD4BF" filter="url(#anim-glow)"><animateMotion dur="2s" repeatCount="indefinite" :begin="2.5 + (i-1)*2/3 + 's'" path="M 610 490 L 750 490 L 900 400" /><animate attributeName="opacity" values="0;1;1;0" dur="2s" repeatCount="indefinite" :begin="2.5 + (i-1)*2/3 + 's'" /></circle></g>
        <g><circle v-for="i in 2" :key="'p9-'+i" r="6" fill="#34D399" filter="url(#anim-glow)"><animateMotion dur="1.5s" repeatCount="indefinite" :begin="3 + (i-1)*1.5/2 + 's'" path="M 1060 400 L 1110 300" /><animate attributeName="opacity" values="0;1;1;0" dur="1.5s" repeatCount="indefinite" :begin="3 + (i-1)*1.5/2 + 's'" /></circle></g>
        <g><circle v-for="i in 5" :key="'p10-'+i" r="6" fill="#4ADE80" filter="url(#anim-glow)"><animateMotion dur="4s" repeatCount="indefinite" :begin="3.5 + (i-1)*4/5 + 's'" path="M 900 260 Q 500 640 155 340" /><animate attributeName="opacity" values="0;1;1;0" dur="4s" repeatCount="indefinite" :begin="3.5 + (i-1)*4/5 + 's'" /></circle></g>
        
        <!-- Training -> ETL Pulsing Rings -->
        <g>
          <circle v-for="i in 3" :key="'p-train-'+i" r="6" fill="none" stroke="#EC4899" stroke-width="2">
            <animateMotion dur="3s" repeatCount="indefinite" :begin="(i-1)*1 + 's'" path="M 535 550 Q 430 550 430 480 L 430 300 Q 430 290 340 290" />
            <animate attributeName="r" values="3;8;3" dur="1s" repeatCount="indefinite" />
            <animate attributeName="opacity" values="0;1;1;0" dur="3s" repeatCount="indefinite" :begin="(i-1)*1 + 's'" />
          </circle>
        </g>
      </g>

    </svg>

    <!-- Controls Bottom Right -->
    <div class="absolute bottom-4 right-4 flex gap-2">
      <button
        @click="togglePlay"
        class="px-2 py-1 rounded-md font-medium transition-all flex items-center gap-1 text-[10px]"
        :class="isPlaying ? 'bg-green-600/80 text-white' : 'bg-slate-700/80 text-slate-300'"
      >
        {{ isPlaying ? '⏸️' : '▶️' }}
      </button>
      <button
        @click="toggleLabels"
        class="px-2 py-1 rounded-md font-medium transition-all text-[10px]"
        :class="showLabels ? 'bg-blue-600/80 text-white' : 'bg-slate-700/80 text-slate-300'"
      >
        🏷️ {{ showLabels ? 'ON' : 'OFF' }}
      </button>
    </div>
  </div>
</template>

<style scoped>
/* Ensure the diagram container takes up available space properly */
:deep(svg) {
  display: block;
}
</style>
