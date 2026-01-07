<script setup lang="ts">
// Static Step-by-Step Architecture Diagram
// Uses native Slidev v-click directives for revealing elements
</script>

<template>
  <div class="relative w-full h-full bg-transparent text-white overflow-hidden">
    
    <!-- Main Diagram SVG - ViewBox 1250x650 -->
    <svg viewBox="0 0 1280 720" class="w-full h-full block">
      <defs>
        <!-- Gradients -->
        <linearGradient id="static-grad-bg" x1="0%" y1="0%" x2="100%" y2="100%">
          <stop offset="0%" stop-color="#1E293B" />
          <stop offset="100%" stop-color="#0F172A" />
        </linearGradient>
        <linearGradient id="static-grad-box" x1="0%" y1="0%" x2="0%" y2="100%">
          <stop offset="0%" stop-color="#334155" />
          <stop offset="100%" stop-color="#1E293B" />
        </linearGradient>
      </defs>

      <!-- Background -->
      <rect width="1280" height="720" fill="url(#static-grad-bg)" />
      
      <!-- Grid pattern -->
      <pattern id="grid" width="30" height="30" patternUnits="userSpaceOnUse">
        <path d="M 30 0 L 0 0 0 30" fill="none" stroke="rgba(148,163,184,0.05)" stroke-width="1"/>
      </pattern>
      <rect width="1280" height="720" fill="url(#grid)" />

      <!-- ========== COLUMN 1: ERP LAYER ========== -->
      
      <!-- Label -->
      <g v-click="1" class="transition-opacity duration-500">
        <rect x="20" y="80" width="160" height="40" rx="8" fill="rgba(124, 58, 237, 0.15)" stroke="#7C3AED" stroke-width="1" stroke-dasharray="4,2" />
        <text x="100" y="100" font-size="5" fill="#A78BFA" text-anchor="middle" dominant-baseline="middle" font-weight="bold">ERP LAYER</text>
      </g>
      
      <!-- Dynamics AX -->
      <g v-click="2" class="transition-opacity duration-500">
        <rect x="25" y="140" width="160" height="200" rx="10" fill="url(#static-grad-box)" stroke="#7C3AED" stroke-width="2" />
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
      </g>

      <!-- Future ERP -->
      <g v-click="3" class="transition-opacity duration-500">
        <g opacity="0.4">
          <rect x="25" y="380" width="160" height="60" rx="10" fill="transparent" stroke="#A78BFA" stroke-width="1" stroke-dasharray="6,3" />
          <text x="105" y="408" font-size="4" fill="#A78BFA" text-anchor="middle">Future ERP</text>
          <text x="105" y="425" font-size="3" fill="#A78BFA" text-anchor="middle">(Upgrade Ready)</text>
        </g>
      </g>

      <!-- ========== COLUMN 2: DEVELOPMENT SCOPE ========== -->

      <!-- Boundary & Label -->
      <g v-click="4" class="transition-opacity duration-500">
        <rect x="260" y="80" width="620" height="560" rx="16" fill="rgba(236, 72, 153, 0.05)" stroke="#EC4899" stroke-width="2" stroke-dasharray="10,5" />
        <rect x="260" y="80" width="620" height="35" rx="16" fill="rgba(236, 72, 153, 0.15)" />
        <text x="570" y="104" font-size="5" fill="#F472B6" text-anchor="middle" font-weight="bold">
          📦 DEVELOPMENT SCOPE — RV &amp; Akshay Team
        </text>
      </g>

      <!-- ETL Services -->
      <g v-click="5" class="transition-opacity duration-500">
        <rect x="280" y="190" width="120" height="100" rx="10" fill="url(#static-grad-box)" stroke="#6366F1" stroke-width="2" />
        <rect x="280" y="190" width="120" height="28" rx="10" fill="#6366F1" />
        <text x="290" y="210" font-size="4.5">⚙️</text>
        <text x="310" y="210" font-size="4.5" fill="white" font-weight="bold">ETL</text>
        <!-- .NET Tag -->
        <rect x="362" y="274" width="32" height="12" rx="6" fill="rgba(255,255,255,0.2)" />
        <text x="378" y="282" font-size="2.5" fill="white" text-anchor="middle" dominant-baseline="middle">.NET</text>
        <text x="295" y="235" font-size="3.5" fill="#E2E8F0">• Data Extraction</text>
        <text x="295" y="252" font-size="3.5" fill="#E2E8F0">• Transform</text>
        <text x="295" y="269" font-size="3.5" fill="#E2E8F0">• Load to DB</text>
      </g>

      <!-- n8n Workflows -->
      <g v-click="6" class="transition-opacity duration-500">
        <rect x="280" y="310" width="120" height="85" rx="10" fill="url(#static-grad-box)" stroke="#F97316" stroke-width="2" />
        <rect x="280" y="310" width="120" height="28" rx="10" fill="#F97316" />
        <text x="290" y="330" font-size="4.5">🔄</text>
        <text x="310" y="330" font-size="4.5" fill="white" font-weight="bold">n8n</text>
        <text x="295" y="358" font-size="3.5" fill="#E2E8F0">• No-Code Logic</text>
        <text x="295" y="375" font-size="3.5" fill="#E2E8F0">• Orchestration</text>
      </g>

      <!-- PostgreSQL -->
      <g v-click="7" class="transition-opacity duration-500">
        <rect x="460" y="240" width="150" height="130" rx="10" fill="url(#static-grad-box)" stroke="#0EA5E9" stroke-width="2" />
        <rect x="460" y="240" width="150" height="28" rx="10" fill="#0EA5E9" />
        <text x="470" y="260" font-size="4.5">🗄️</text>
        <text x="490" y="260" font-size="4.5" fill="white" font-weight="bold">PostgreSQL</text>
        <!-- DB Tag -->
        <rect x="579" y="354" width="20" height="12" rx="6" fill="rgba(255,255,255,0.2)" />
        <text x="589" y="362" font-size="2.5" fill="white" text-anchor="middle" dominant-baseline="middle">DB</text>
        <text x="475" y="288" font-size="3.5" fill="#E2E8F0">• Central Database</text>
        <text x="475" y="305" font-size="3.5" fill="#E2E8F0">• Order States</text>
        <text x="475" y="322" font-size="3.5" fill="#E2E8F0">• Driver Data</text>
        <text x="475" y="339" font-size="3.5" fill="#E2E8F0">• Analytics Store</text>
      </g>

      <!-- Microservices -->
      <g v-click="8" class="transition-opacity duration-500">
        <rect x="460" y="420" width="150" height="100" rx="10" fill="url(#static-grad-box)" stroke="#8B5CF6" stroke-width="2" />
        <rect x="460" y="420" width="150" height="28" rx="10" fill="#8B5CF6" />
        <text x="470" y="440" font-size="4.5">🔧</text>
        <text x="490" y="440" font-size="4.5" fill="white" font-weight="bold">Microservices</text>
        <!-- .NET Tag -->
        <rect x="574" y="504" width="32" height="12" rx="6" fill="rgba(255,255,255,0.2)" />
        <text x="590" y="512" font-size="2.5" fill="white" text-anchor="middle" dominant-baseline="middle">.NET</text>
        <text x="475" y="468" font-size="3.5" fill="#E2E8F0">• Business Logic</text>
        <text x="475" y="485" font-size="3.5" fill="#E2E8F0">• API Gateway</text>
        <text x="475" y="502" font-size="3.5" fill="#E2E8F0">• State Mgmt</text>
      </g>

      <!-- FastAPI -->
      <g v-click="9" class="transition-opacity duration-500">
        <rect x="680" y="240" width="140" height="100" rx="10" fill="url(#static-grad-box)" stroke="#10B981" stroke-width="2" />
        <rect x="680" y="240" width="140" height="28" rx="10" fill="#10B981" />
        <text x="690" y="260" font-size="4.5">⚡</text>
        <text x="710" y="260" font-size="4.5" fill="white" font-weight="bold">FastAPI</text>
        <!-- PYTHON Tag -->
        <rect x="775" y="324" width="42" height="12" rx="6" fill="rgba(255,255,255,0.2)" />
        <text x="796" y="332" font-size="2.5" fill="white" text-anchor="middle" dominant-baseline="middle">PYTHON</text>
        <text x="695" y="288" font-size="3.5" fill="#E2E8F0">• REST APIs</text>
        <text x="695" y="305" font-size="3.5" fill="#E2E8F0">• AI Inference</text>
        <text x="695" y="322" font-size="3.5" fill="#E2E8F0">• Real-time</text>
      </g>

      <!-- AI Models -->
      <g v-click="10" class="transition-opacity duration-500">
        <rect x="680" y="360" width="140" height="130" rx="10" fill="url(#static-grad-box)" stroke="#F59E0B" stroke-width="2" />
        <rect x="680" y="360" width="140" height="28" rx="10" fill="#F59E0B" />
        <text x="690" y="380" font-size="4.5">🧠</text>
        <text x="710" y="380" font-size="4.5" fill="white" font-weight="bold">AI Models</text>

        <text x="695" y="410" font-size="3.5" fill="#E2E8F0">• Route Optimization</text>
        <text x="695" y="427" font-size="3.5" fill="#E2E8F0">• Smart Allocation</text>
        <text x="695" y="444" font-size="3.5" fill="#E2E8F0">• Predictions</text>
        <text x="695" y="461" font-size="3.5" fill="#E2E8F0">• Training Pipeline</text>
        
        <!-- Edison Badge -->
        <rect x="707.5" y="495" width="85" height="22" rx="11" fill="#F59E0B" />
        <text x="750" y="506" font-size="3.5" fill="white" text-anchor="middle" dominant-baseline="middle" font-weight="bold">💡 EDISON</text>
      </g>

      <!-- Training / Testing -->
      <g v-click="11" class="transition-opacity duration-500">
        <rect x="460" y="550" width="150" height="70" rx="10" fill="url(#static-grad-box)" stroke="#EC4899" stroke-width="2" />
        <rect x="460" y="550" width="150" height="28" rx="10" fill="#EC4899" />
        <text x="470" y="570" font-size="4.5">🔬</text>
        <text x="490" y="570" font-size="4.5" fill="white" font-weight="bold">Training</text>
        <text x="475" y="598" font-size="3.5" fill="#E2E8F0">• Model Training</text>
        <text x="475" y="615" font-size="3.5" fill="#E2E8F0">• Validation</text>
      </g>

      <!-- ========== COLUMN 3: FRONTEND APPS ========== -->

      <!-- Label -->
      <g v-click="12" class="transition-opacity duration-500">
        <rect x="900" y="80" width="180" height="40" rx="8" fill="rgba(59, 130, 246, 0.15)" stroke="#3B82F6" stroke-width="1" stroke-dasharray="4,2" />
        <text x="990" y="100" font-size="5" fill="#60A5FA" text-anchor="middle" dominant-baseline="middle" font-weight="bold">FRONTEND APPS</text>
      </g>
      
      <!-- Driver App -->
      <g v-click="13" class="transition-opacity duration-500">
        <rect x="900" y="150" width="180" height="140" rx="10" fill="url(#static-grad-box)" stroke="#3B82F6" stroke-width="2" />
        <rect x="900" y="150" width="180" height="28" rx="10" fill="#3B82F6" />
        <text x="910" y="170" font-size="4.5">📱</text>
        <text x="930" y="170" font-size="4.5" fill="white" font-weight="bold">Driver App</text>
        <!-- FLUTTER Tag -->
        <rect x="1026" y="274" width="48" height="14" rx="6" fill="rgba(255,255,255,0.2)" />
        <text x="1050" y="282" font-size="2.5" fill="white" text-anchor="middle" dominant-baseline="middle">FLUTTER</text>
        <text x="915" y="198" font-size="3.5" fill="#E2E8F0">• iOS + Android</text>
        <text x="915" y="215" font-size="3.5" fill="#E2E8F0">• Offline Support</text>
        <text x="915" y="232" font-size="3.5" fill="#E2E8F0">• GPS Tracking</text>
        <text x="915" y="249" font-size="3.5" fill="#E2E8F0">• POD Capture</text>
        <text x="915" y="266" font-size="3.5" fill="#E2E8F0">• Chat</text>
        
        <!-- Hot Wheels Badge -->
        <rect x="940" y="295" width="120" height="22" rx="11" fill="#EF4444" />
        <text x="1000" y="306" font-size="3.5" fill="white" text-anchor="middle" dominant-baseline="middle" font-weight="bold">🚗 HOT WHEELS</text>
      </g>

      <!-- Analytics Portal -->
      <g v-click="14" class="transition-opacity duration-500">
        <rect x="900" y="340" width="180" height="120" rx="10" fill="url(#static-grad-box)" stroke="#14B8A6" stroke-width="2" />
        <rect x="900" y="340" width="180" height="28" rx="10" fill="#14B8A6" />
        <text x="910" y="360" font-size="4.5">🖥️</text>
        <text x="930" y="360" font-size="4.5" fill="white" font-weight="bold">Analytics Portal</text>
        <!-- WEB Tag -->
        <rect x="1041" y="444" width="28" height="12" rx="6" fill="rgba(255,255,255,0.2)" />
        <text x="1055" y="452" font-size="2.5" fill="white" text-anchor="middle" dominant-baseline="middle">WEB</text>
        <text x="915" y="388" font-size="3.5" fill="#E2E8F0">• Control Tower</text>
        <text x="915" y="405" font-size="3.5" fill="#E2E8F0">• Real-time Map</text>
        <text x="915" y="422" font-size="3.5" fill="#E2E8F0">• Dispatch Console</text>
        <text x="915" y="439" font-size="3.5" fill="#E2E8F0">• Reports</text>
        
        <!-- Eagle Badge -->
        <rect x="940" y="465" width="85" height="22" rx="11" fill="#14B8A6" />
        <text x="982.5" y="476" font-size="3.5" fill="white" text-anchor="middle" dominant-baseline="middle" font-weight="bold">🦅 EAGLE</text>
      </g>

      <!-- ========== COLUMN 4: COMMS ========== -->
      
      <!-- Label -->
      <g v-click="15" class="transition-opacity duration-500">
        <rect x="1110" y="80" width="100" height="40" rx="8" fill="rgba(16, 185, 129, 0.15)" stroke="#10B981" stroke-width="1" stroke-dasharray="4,2" />
        <text x="1160" y="100" font-size="5" fill="#34D399" text-anchor="middle" dominant-baseline="middle" font-weight="bold">COMMS</text>
      </g>

      <!-- Teams API -->
      <g v-click="16" class="transition-opacity duration-500">
        <rect x="1110" y="150" width="120" height="70" rx="10" fill="url(#static-grad-box)" stroke="#7C3AED" stroke-width="2" />
        <rect x="1110" y="150" width="120" height="24" rx="10" fill="#7C3AED" />
        <text x="1120" y="167" font-size="4.5">👥</text>
        <text x="1136" y="167" font-size="4.5" fill="white" font-weight="bold">Teams</text>
        <text x="1122" y="190" font-size="3.5" fill="#E2E8F0">• Status Updates</text>
        <text x="1122" y="205" font-size="3.5" fill="#E2E8F0">• ETL Triggers</text>
      </g>

      <!-- Alerts / Communication -->
      <g v-click="17" class="transition-opacity duration-500">
        <rect x="1110" y="240" width="120" height="120" rx="10" fill="url(#static-grad-box)" stroke="#10B981" stroke-width="2" />
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
      </g>

    </svg>
  </div>
</template>

<style scoped>
:deep(svg) {
  display: block;
}
</style>
