<script setup>
import { ref } from 'vue';
import Icon from './components/Icon.vue';

// Mock Data for Feature 1: Guidance Tracker
const guidanceMetrics = ref([
    {
        id: 1,
        metric: "H100 Supply Lead Time",
        source: "Q1 Earnings Call (Promise)",
        promise: "Decreasing to 20-24 weeks",
        reality: "28 weeks (Channel Check)",
        status: "Diverging", // Diverging, On Track
        impact: "High",
        lastUpdated: "Today, 9:30 AM",
        trend: "worsening"
    },
    {
        id: 2,
        metric: "Gross Margin Input (Copper)",
        source: "CFO Guidance",
        promise: "Stable Costs",
        reality: "Copper +15% since earnings",
        status: "Warning",
        impact: "Medium",
        lastUpdated: "Live Market Data",
        trend: "worsening"
    },
    {
        id: 3,
        metric: "China Market Revenue",
        source: "CEO Outlook",
        promise: "Recovering via H20 chips",
        reality: "Export License Delays (News)",
        status: "Critical",
        impact: "High",
        lastUpdated: "2 hours ago",
        trend: "worsening"
    }
]);

// Mock Data for Feature 3: Narrative Drift
const narrativeEvents = ref([
    {
        id: 1,
        date: "Today",
        event: "Goldman Sachs Tech Conf",
        speaker: "Jensen Huang (CEO)",
        quote: "...we are seeing some pause in datacenter build-outs as customers await Blackwell...",
        sentiment: 4.5, // 0-10
        drift: "Negative Shift",
        comparison: "Contrast this with Q1 Earnings: 'Demand is insatiable, no pause expected.'",
        tags: ["Demand", "CapEx"]
    },
    {
        id: 2,
        date: "5 Days Ago",
        event: "8-K Filing (Partnership)",
        speaker: "Official Filing",
        quote: "Expanded partnership with Oracle for sovereign AI cloud...",
        sentiment: 8.0,
        drift: "Consistent",
        comparison: "Aligns with 'Sovereign AI' thesis from earnings.",
        tags: ["Growth", "Cloud"]
    },
    {
        id: 3,
        date: "May 22 (Baseline)",
        event: "Q1 Earnings Call",
        speaker: "Jensen Huang (CEO)",
        quote: "We are at the beginning of a new industrial revolution. Demand is well ahead of supply.",
        sentiment: 9.5,
        drift: "Baseline",
        comparison: "Reference Point",
        tags: ["Macro", "Vision"]
    }
]);
</script>

<template>
  <div class="min-h-screen font-sans selection:bg-cyan-500 selection:text-white pb-20 bg-slate-900 text-slate-200">
    <!-- Header -->
    <header class="border-b border-slate-800 bg-slate-900/50 sticky top-0 z-50 backdrop-blur-md">
        <div class="max-w-7xl mx-auto px-6 h-16 flex items-center justify-between">
            <div class="flex items-center space-x-2">
                <div class="w-8 h-8 bg-cyan-500 rounded-lg flex items-center justify-center">
                    <span class="font-bold text-slate-900">AD</span>
                </div>
                <span class="font-bold text-xl tracking-tight text-white">AlphaDecode</span>
                <span class="text-xs bg-cyan-900 text-cyan-300 px-2 py-0.5 rounded-full border border-cyan-700/50">Pro</span>
            </div>
            <div class="flex items-center space-x-6">
                <nav className="hidden md:flex space-x-6 text-sm font-medium text-slate-400">
                    <a href="#" class="text-white">Dashboard</a>
                    <a href="#" class="hover:text-white transition-colors">Watchlist</a>
                    <a href="#" class="hover:text-white transition-colors">Screener</a>
                </nav>
                <div class="w-8 h-8 rounded-full bg-slate-700 border border-slate-600"></div>
            </div>
        </div>
    </header>

    <!-- Ticker Header -->
    <div class="bg-slate-900 border-b border-slate-800">
        <div class="max-w-7xl mx-auto px-6 py-6">
            <div class="flex items-start justify-between">
                <div>
                    <div class="flex items-center space-x-3">
                        <h1 class="text-4xl font-bold text-white">NVDA</h1>
                        <span class="text-slate-400 text-lg">NVIDIA Corp.</span>
                        <span class="text-red-400 bg-red-400/10 px-2 py-1 rounded text-sm font-mono border border-red-400/20">-1.2% Today</span>
                    </div>
                    <div class="mt-2 flex items-center space-x-2 text-sm text-slate-400">
                        <span>AI Narrative Health:</span>
                        <div class="h-2 w-24 bg-slate-700 rounded-full overflow-hidden">
                            <div class="h-full w-2/3 bg-yellow-500"></div>
                        </div>
                        <span class="text-yellow-500 font-medium">Cautious (6.5/10)</span>
                    </div>
                </div>
                <div class="flex space-x-3">
                    <button class="px-4 py-2 bg-slate-800 hover:bg-slate-700 text-white rounded-lg border border-slate-700 transition-colors text-sm font-medium">
                        + Watchlist
                    </button>
                    <button class="px-4 py-2 bg-cyan-600 hover:bg-cyan-500 text-white rounded-lg shadow-lg shadow-cyan-500/20 transition-colors text-sm font-medium">
                        Full Report
                    </button>
                </div>
            </div>
        </div>
    </div>

    <main class="max-w-7xl mx-auto px-6 py-8 grid grid-cols-1 lg:grid-cols-12 gap-8">
        
        <!-- LEFT COLUMN: Guidance Reality Check (Feature 1) -->
        <div class="lg:col-span-5 space-y-6">
            <div class="flex items-center justify-between mb-2">
                <h2 class="text-lg font-semibold text-white flex items-center gap-2">
                    <Icon name="Activity" color="#22d3ee" />
                    Guidance Reality Check
                </h2>
                <span class="text-xs text-slate-500">Updated: Real-time</span>
            </div>
            
            <p class="text-sm text-slate-400 mb-4">
                Monitoring <span class="text-white font-medium">3 key promises</span> made in the Q1 Earnings Call against live external data.
            </p>

            <div class="space-y-4">
                <div v-for="item in guidanceMetrics" :key="item.id" class="glass-panel p-5 rounded-xl border-l-4 border-l-red-500 hover:bg-slate-800/50 transition-all cursor-pointer group">
                    <div class="flex justify-between items-start mb-3">
                        <h3 class="font-semibold text-slate-200">{{ item.metric }}</h3>
                        <span class="text-xs font-bold px-2 py-1 rounded uppercase tracking-wider"
                              :class="{
                                  'bg-red-500/10 text-red-400 border border-red-500/20': item.status === 'Diverging',
                                  'bg-red-900/20 text-red-500 border border-red-500/30': item.status === 'Critical',
                                  'bg-yellow-500/10 text-yellow-400 border border-yellow-500/20': item.status !== 'Diverging' && item.status !== 'Critical'
                              }">
                            {{ item.status }}
                        </span>
                    </div>
                    
                    <div class="grid grid-cols-2 gap-4 mb-4">
                        <div class="space-y-1">
                            <p class="text-xs text-slate-500 uppercase tracking-wider">Management Promised</p>
                            <p class="text-sm text-slate-300 border-l-2 border-slate-600 pl-2">{{ item.promise }}</p>
                        </div>
                        <div class="space-y-1">
                            <p class="text-xs text-cyan-500 uppercase tracking-wider">Current Reality</p>
                            <p class="text-sm text-white font-medium border-l-2 border-cyan-500 pl-2">{{ item.reality }}</p>
                        </div>
                    </div>
                    
                    <div class="flex items-center justify-between pt-3 border-t border-slate-800">
                        <span class="text-xs text-slate-500">Impact: <span class="text-white">{{ item.impact }}</span></span>
                        <span class="text-xs text-cyan-400 group-hover:translate-x-1 transition-transform flex items-center gap-1">
                            Analyze Source <Icon name="ArrowRight" :size="12" />
                        </span>
                    </div>
                </div>
            </div>
            
            <div class="bg-slate-800/30 p-4 rounded-lg border border-slate-700 text-center">
                <p class="text-sm text-slate-400">Want to track Supply Chain data deeper?</p>
                <button class="mt-2 text-cyan-400 text-sm font-medium hover:underline">Upgrade to Supply Chain Pro &rarr;</button>
            </div>
        </div>

        <!-- RIGHT COLUMN: Narrative Drift (Feature 3) -->
        <div class="lg:col-span-7 space-y-6">
             <div class="flex items-center justify-between mb-2">
                <h2 class="text-lg font-semibold text-white flex items-center gap-2">
                    <Icon name="TrendingDown" color="#f472b6" />
                    Narrative Drift & Silent Updates
                </h2>
                <div class="flex gap-2">
                    <span class="px-2 py-1 bg-slate-800 text-xs text-slate-400 rounded hover:text-white cursor-pointer">All</span>
                    <span class="px-2 py-1 bg-cyan-900/30 text-xs text-cyan-400 rounded border border-cyan-800 hover:bg-cyan-900/50 cursor-pointer">Divergence Only</span>
                </div>
            </div>

            <div class="relative pl-6 border-l border-slate-800 space-y-8">
                <div v-for="(event, idx) in narrativeEvents" :key="event.id" class="relative">
                    <!-- Timeline Dot -->
                    <div class="absolute -left-[29px] top-2 w-4 h-4 rounded-full border-2"
                         :class="{
                             'bg-red-500 border-slate-900 shadow-[0_0_10px_rgba(239,68,68,0.5)]': idx === 0,
                             'bg-slate-600 border-slate-900': idx === narrativeEvents.length - 1,
                             'bg-slate-700 border-slate-900': idx !== 0 && idx !== narrativeEvents.length - 1
                         }"></div>

                    <div class="glass-panel p-6 rounded-xl" :class="{ 'border-t-2 border-t-red-500': idx === 0 }">
                        <div class="flex justify-between items-start mb-2">
                            <div>
                                <div class="flex items-center gap-2">
                                    <span class="text-xs font-mono text-cyan-400 bg-cyan-950 px-1.5 py-0.5 rounded">{{ event.date }}</span>
                                    <span class="text-sm font-medium text-slate-300">{{ event.event }}</span>
                                </div>
                                <h4 class="text-white font-medium mt-1">{{ event.speaker }}</h4>
                            </div>
                            <span v-if="event.drift !== 'Baseline'" class="text-xs font-bold px-2 py-1 rounded"
                                  :class="event.drift.includes('Negative') ? 'bg-red-500/20 text-red-400' : 'bg-green-500/20 text-green-400'">
                                {{ event.drift }}
                            </span>
                        </div>

                        <div class="bg-slate-950/50 p-4 rounded-lg border border-slate-800 mb-3 italic text-slate-300 relative">
                            <span class="absolute top-2 left-2 text-slate-700 text-4xl leading-none">"</span>
                            <p class="relative z-10 pl-4">{{ event.quote }}</p>
                        </div>

                        <div v-if="event.drift !== 'Baseline'" class="bg-red-950/20 p-3 rounded border border-red-900/30 flex items-start gap-3">
                            <div class="mt-0.5"><Icon name="AlertTriangle" color="#ef4444" /></div>
                            <div>
                                <p class="text-sm font-bold text-red-400 mb-1">AI Narrative Alert:</p>
                                <p class="text-sm text-slate-400">{{ event.comparison }}</p>
                            </div>
                        </div>
                        
                        <div class="mt-3 flex gap-2">
                            <span v-for="tag in event.tags" :key="tag" class="text-xs text-slate-500 bg-slate-800 px-2 py-1 rounded hover:text-slate-300 cursor-pointer">#{{ tag }}</span>
                        </div>
                    </div>
                </div>
            </div>
        </div>
    </main>
  </div>
</template>
