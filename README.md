<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Effective Verifier Interview - Practical Training Module</title>
    <!-- Tailwind CSS CDN -->
    <script src="https://cdn.tailwindcss.com"></script>
    <!-- Chart.js CDN -->
    <script src="https://cdn.jsdelivr.net/npm/chart.js"></script>
    <script>
        tailwind.config = {
            theme: {
                extend: {
                    colors: {
                        brand: {
                            50: '#FDFBF7',
                            100: '#F7F3EB',
                            200: '#EFE6D5',
                            500: '#D97706',
                            600: '#C2410C',
                            700: '#9A3412',
                            800: '#1E293B',
                            900: '#0F172A',
                        },
                        sage: {
                            50: '#F0FDF4',
                            100: '#DCFCE7',
                            500: '#10B981',
                            700: '#047857',
                            800: '#065F46',
                        }
                    }
                }
            }
        }
    </script>
    <style>
        .chart-container {
            position: relative;
            width: 100%;
            max-width: 550px;
            margin-left: auto;
            margin-right: auto;
            height: 280px;
            max-height: 320px;
        }
        @media (min-width: 768px) {
            .chart-container {
                height: 320px;
            }
        }
        /* Custom scrollbar for inner tab containers */
        .custom-scrollbar::-webkit-scrollbar {
            width: 6px;
            height: 6px;
        }
        .custom-scrollbar::-webkit-scrollbar-track {
            background: #F1F5F9;
            border-radius: 4px;
        }
        .custom-scrollbar::-webkit-scrollbar-thumb {
            background: #CBD5E1;
            border-radius: 4px;
        }
        .custom-scrollbar::-webkit-scrollbar-thumb:hover {
            background: #94A3B8;
        }
    </style>
</head>
<body class="bg-brand-50 text-slate-800 font-sans antialiased selection:bg-amber-200 selection:text-amber-900 min-h-screen flex flex-col">

    <!-- Chosen Palette: Warm Neutral Harmony (Warm Sand Background #FDFBF7, Deep Slate Primary #1E293B, Terracotta/Amber Accents #C2410C / #D97706, Sage Green Details #047857) -->
    <!-- Application Structure Plan:
         The application is designed as an interactive, practical workshop companion divided into 6 functional sections:
         1. Executive Dashboard & Interactive Agenda: Gives trainers and participants an instant overview of the 2.5-hour roadmap, protected time blocks, and learning outcomes with dynamic visual time allocation.
         2. Practical Standard & Question Builder: Translates the Ask-Listen-Record standard and provides an interactive step-by-step Question Construction Tool where teams turn desktop review gaps into compliant questions using the 3-pattern framework.
         3. Interactive Trainer Demonstration: A side-by-side script simulator contrasting weak vs. effective interviewing with pause-and-reflect prompts to make the standard visible before practice.
         4. Activity 2 Coached Practice Suite: Features interactive role assigners, a live practice timer with session stages, and a dynamic digital Observer Checklist (Appendix B) with real-time feedback tallying.
         5. Reference Library & Difficult Situations Matrix: Searchable/filterable Do's, Don'ts, and situational handling strategies for live interview challenges.
         6. Mock Readiness & Appendix Generator: Interactive 5-check readiness tool, post-interview debrief separator, and interactive Appendix A sheet ready for print/saving.
         This non-linear design empowers facilitators to project/manage the session and allows verifier teams to interactively prepare and document their work in real-time. -->
    <!-- Visualization & Content Choices:
         - Session Plan Time Allocation: Chart.js Donut Chart -> Visualizes protected practice time vs lecture time -> Confirming 75% time spent in practice/demo.
         - Ask-Listen-Record Evidence Cycle: Custom HTML/CSS Interactive Tri-Fold Cards -> Click to reveal specific behaviors and verifier tips.
         - Trainer Demonstration Weak vs Effective: Dynamic Toggle Script Player -> Audio/Visual text playback mode with reflection prompt.
         - Practice Round Stage Timer: Vanilla JS Countdown Clock with phase indicators -> Keeps Activity 2 tightly managed.
         - Appendix B Observer Checklist: Interactive Rating Form with auto-summary score & feedback builder.
         - Appendix A Planning Sheet: Interactive Form with instant printable/exportable preview -> Saves team work for mock session.
         - CONFIRMATION: NO SVG graphics used. NO Mermaid JS used. All visuals rely on HTML5 Canvas (Chart.js) or CSS3/Tailwind UI elements. -->
    <!-- CONFIRMATION: NO SVG graphics used. NO Mermaid JS used. -->

    <!-- TOP NAVIGATION BAR -->
    <header class="sticky top-0 z-50 bg-slate-900 text-white shadow-md border-b border-slate-700">
        <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
            <div class="flex items-center justify-between h-16">
                <div class="flex items-center space-x-3">
                    <div class="bg-amber-500 text-slate-950 font-black text-lg px-2.5 py-1 rounded shadow-sm">TA10</div>
                    <div>
                        <h1 class="text-base sm:text-lg font-bold leading-tight text-white">Effective Verifier Interview</h1>
                        <p class="text-xs text-slate-300 hidden sm:block">Practical Training Module & Workstation • 22 August 2026</p>
                    </div>
                </div>
                <nav class="hidden md:flex space-x-1 text-xs font-semibold">
                    <button onclick="switchTab('dashboard')" id="nav-dashboard" class="nav-btn px-3 py-2 rounded-md hover:bg-slate-800 transition text-amber-400 bg-slate-800">Dashboard & Agenda</button>
                    <button onclick="switchTab('standard')" id="nav-standard" class="nav-btn px-3 py-2 rounded-md hover:bg-slate-800 transition text-slate-300">Standard & Questions</button>
                    <button onclick="switchTab('demo')" id="nav-demo" class="nav-btn px-3 py-2 rounded-md hover:bg-slate-800 transition text-slate-300">Trainer Demo</button>
                    <button onclick="switchTab('practice')" id="nav-practice" class="nav-btn px-3 py-2 rounded-md hover:bg-slate-800 transition text-slate-300">Practice & Timer</button>
                    <button onclick="switchTab('toolkit')" id="nav-toolkit" class="nav-btn px-3 py-2 rounded-md hover:bg-slate-800 transition text-slate-300">Reference Toolkit</button>
                    <button onclick="switchTab('appendices')" id="nav-appendices" class="nav-btn px-3 py-2 rounded-md hover:bg-slate-800 transition text-slate-300">Appendices & Mock Prep</button>
                </nav>
                <div class="md:hidden">
                    <select id="mobile-nav" onchange="switchTab(this.value)" class="bg-slate-800 text-amber-400 text-xs font-bold rounded px-2 py-1.5 border border-slate-700">
                        <option value="dashboard">1. Dashboard & Agenda</option>
                        <option value="standard">2. Standard & Questions</option>
                        <option value="demo">3. Trainer Demo</option>
                        <option value="practice">4. Practice & Timer</option>
                        <option value="toolkit">5. Reference Toolkit</option>
                        <option value="appendices">6. Appendices & Prep</option>
                    </select>
                </div>
            </div>
        </div>
    </header>

    <!-- MAIN CONTAINER -->
    <main class="flex-grow max-w-7xl w-full mx-auto px-4 sm:px-6 lg:px-8 py-6">

        <!-- ================= SECTION 1: DASHBOARD & AGENDA ================= -->
        <section id="sec-dashboard" class="tab-content space-y-6">
            <!-- Intro Paragraph -->
            <div class="bg-white rounded-xl p-6 shadow-sm border border-slate-200">
                <div class="flex flex-col lg:flex-row lg:items-center justify-between gap-4">
                    <div>
                        <div class="inline-flex items-center px-2.5 py-0.5 rounded-full text-xs font-bold bg-amber-100 text-amber-800 mb-2">
                            Session Duration: 150 Minutes (08:00 - 10:30)
                        </div>
                        <h2 class="text-2xl font-bold text-slate-900">Practical Verifier Interview Training Workstation</h2>
                        <p class="text-slate-600 text-sm mt-1 max-w-3xl">
                            This module prepares verifier teams to conduct focused, respectful, and evidence-based stakeholder interviews. Starting from desktop review findings (VT1–VT4 & SVR), teams build actionable questions, participate in a coached mock interview, and leave ready for official verification sessions.
                        </p>
                    </div>
                    <div class="flex flex-wrap gap-2 text-center">
                        <div class="bg-amber-50 border border-amber-200 rounded-lg p-3 min-w-[110px]">
                            <span class="block text-2xl font-black text-amber-700">2</span>
                            <span class="text-xs text-amber-900 font-medium">Core Activities</span>
                        </div>
                        <div class="bg-slate-50 border border-slate-200 rounded-lg p-3 min-w-[110px]">
                            <span class="block text-2xl font-black text-slate-800">3</span>
                            <span class="text-xs text-slate-600 font-medium">Max Questions</span>
                        </div>
                        <div class="bg-emerald-50 border border-emerald-200 rounded-lg p-3 min-w-[110px]">
                            <span class="block text-2xl font-black text-emerald-700">75 min</span>
                            <span class="text-xs text-emerald-900 font-medium">Protected Practice</span>
                        </div>
                    </div>
                </div>
            </div>

            <!-- Dashboard Grid: Timeline & Learning Outcomes -->
            <div class="grid grid-cols-1 lg:grid-cols-12 gap-6">
                <!-- Left Column: Session Agenda Table & Timeline -->
                <div class="lg:col-span-8 bg-white rounded-xl p-6 shadow-sm border border-slate-200 flex flex-col">
                    <h3 class="text-lg font-bold text-slate-900 mb-1 flex items-center justify-between">
                        <span>2.5-Hour Trainer-Ready Sequence</span>
                        <span class="text-xs font-normal text-slate-500">Click any row to jump to feature</span>
                    </h3>
                    <p class="text-xs text-slate-500 mb-4">Protect the 30-min planning, 45-min practice, and 15-min mock prep blocks.</p>
                   
                    <div class="overflow-x-auto custom-scrollbar flex-grow">
                        <table class="w-full text-left text-xs text-slate-700">
                            <thead class="bg-slate-100 text-slate-800 uppercase font-bold text-[11px] border-b border-slate-200">
                                <tr>
                                    <th class="p-3">Time</th>
                                    <th class="p-3">Min</th>
                                    <th class="p-3">Focus</th>
                                    <th class="p-3">Trainer Execution & Activity Focus</th>
                                    <th class="p-3">Immediate Output</th>
                                </tr>
                            </thead>
                            <tbody class="divide-y divide-slate-100">
                                <tr class="hover:bg-amber-50/60 cursor-pointer transition" onclick="switchTab('standard')">
                                    <td class="p-3 font-semibold text-slate-900 whitespace-nowrap">08:00 - 08:15</td>
                                    <td class="p-3 font-bold text-amber-700">15</td>
                                    <td class="p-3 font-semibold">Welcome & Scope</td>
                                    <td class="p-3">Connect to desktop review. Set working rules & check VT1–VT4/SVR materials.</td>
                                    <td class="p-3"><span class="bg-slate-100 text-slate-700 px-2 py-1 rounded font-medium">Scope Confirmed</span></td>
                                </tr>
                                <tr class="hover:bg-amber-50/60 cursor-pointer transition" onclick="switchTab('standard')">
                                    <td class="p-3 font-semibold text-slate-900 whitespace-nowrap">08:15 - 08:35</td>
                                    <td class="p-3 font-bold text-amber-700">20</td>
                                    <td class="p-3 font-semibold">Good Standard</td>
                                    <td class="p-3">Explain Ask-Listen-Record cycle, 6 habits, and Do's & Don'ts with simple model.</td>
                                    <td class="p-3"><span class="bg-slate-100 text-slate-700 px-2 py-1 rounded font-medium">Standard Clear</span></td>
                                </tr>
                                <tr class="hover:bg-amber-50/60 cursor-pointer transition bg-amber-50/30" onclick="switchTab('standard')">
                                    <td class="p-3 font-semibold text-amber-900 whitespace-nowrap">08:35 - 09:05</td>
                                    <td class="p-3 font-bold text-amber-700">30</td>
                                    <td class="p-3 font-semibold text-amber-900">Activity 1: Planning</td>
                                    <td class="p-3 text-slate-800">Teams select 1 desktop priority & draft max 3 questions. Trainer confirms Q1.</td>
                                    <td class="p-3"><span class="bg-amber-100 text-amber-800 px-2 py-1 rounded font-bold">3 Usable Questions</span></td>
                                </tr>
                                <tr class="hover:bg-slate-50">
                                    <td class="p-3 font-semibold text-slate-400 whitespace-nowrap">09:05 - 09:15</td>
                                    <td class="p-3 font-bold text-slate-400">10</td>
                                    <td class="p-3 text-slate-400">Break & Setup</td>
                                    <td class="p-3 text-slate-400">Arrange 5-person practice roles and distribute observer feedback forms.</td>
                                    <td class="p-3"><span class="bg-slate-100 text-slate-500 px-2 py-1 rounded">Roles Assigned</span></td>
                                </tr>
                                <tr class="hover:bg-amber-50/60 cursor-pointer transition" onclick="switchTab('demo')">
                                    <td class="p-3 font-semibold text-slate-900 whitespace-nowrap">09:15 - 09:30</td>
                                    <td class="p-3 font-bold text-amber-700">15</td>
                                    <td class="p-3 font-semibold">Trainer Demo</td>
                                    <td class="p-3">Contrast weak vs. effective approach. Pause for participant reflection.</td>
                                    <td class="p-3"><span class="bg-slate-100 text-slate-700 px-2 py-1 rounded font-medium">Process Visible</span></td>
                                </tr>
                                <tr class="hover:bg-amber-50/60 cursor-pointer transition bg-emerald-50/30" onclick="switchTab('practice')">
                                    <td class="p-3 font-semibold text-emerald-950 whitespace-nowrap">09:30 - 10:15</td>
                                    <td class="p-3 font-bold text-emerald-700">45</td>
                                    <td class="p-3 font-semibold text-emerald-950">Activity 2: Coached Practice</td>
                                    <td class="p-3 text-slate-800">Conduct full interview practice, rapporteur read-back, observer feedback & coaching.</td>
                                    <td class="p-3"><span class="bg-emerald-100 text-emerald-800 px-2 py-1 rounded font-bold">1 Complete Practice</span></td>
                                </tr>
                                <tr class="hover:bg-amber-50/60 cursor-pointer transition bg-slate-50" onclick="switchTab('appendices')">
                                    <td class="p-3 font-semibold text-slate-900 whitespace-nowrap">10:15 - 10:30</td>
                                    <td class="p-3 font-bold text-amber-700">15</td>
                                    <td class="p-3 font-semibold">Mock Prep</td>
                                    <td class="p-3">Confirm priorities, maximum 3 questions, roles, evidence links & readiness check.</td>
                                    <td class="p-3"><span class="bg-slate-200 text-slate-800 px-2 py-1 rounded font-bold">Mock Plan Ready</span></td>
                                </tr>
                            </tbody>
                        </table>
                    </div>
                </div>

                <!-- Right Column: Time Allocation Chart & Learning Outcomes -->
                <div class="lg:col-span-4 space-y-6 flex flex-col">
                    <!-- Chart Card -->
                    <div class="bg-white rounded-xl p-5 shadow-sm border border-slate-200">
                        <h3 class="text-sm font-bold text-slate-900 mb-2">Session Time Distribution (150 min)</h3>
                        <div class="chart-container">
                            <canvas id="agendaChart"></canvas>
                        </div>
                    </div>

                    <!-- Learning Outcomes Card -->
                    <div class="bg-white rounded-xl p-5 shadow-sm border border-slate-200 flex-grow">
                        <h3 class="text-sm font-bold text-slate-900 mb-3 flex items-center gap-2">
                            <span class="w-2 h-2 rounded-full bg-amber-500"></span>
                            Key Learning Outcomes
                        </h3>
                        <ul class="space-y-2 text-xs text-slate-600">
                            <li class="flex items-start gap-2">
                                <span class="text-amber-600 font-bold">✓</span>
                                <span>Select 1 interview priority from VT1-VT4 requirement, SVR statement & evidence matter.</span>
                            </li>
                            <li class="flex items-start gap-2">
                                <span class="text-amber-600 font-bold">✓</span>
                                <span>Prepare no more than 3 clear questions for the selected session.</span>
                            </li>
                            <li class="flex items-start gap-2">
                                <span class="text-amber-600 font-bold">✓</span>
                                <span>Open and close an interview clearly and professionally.</span>
                            </li>
                            <li class="flex items-start gap-2">
                                <span class="text-amber-600 font-bold">✓</span>
                                <span>Apply the <strong>Ask-Listen-Record</strong> cycle and separate responses from evidence shown.</span>
                            </li>
                            <li class="flex items-start gap-2">
                                <span class="text-amber-600 font-bold">✓</span>
                                <span>Debrief as a verifier team without making a premature rating or approval decision.</span>
                            </li>
                        </ul>
                    </div>
                </div>
            </div>
        </section>


        <!-- ================= SECTION 2: STANDARD & QUESTION BUILDER ================= -->
        <section id="sec-standard" class="tab-content hidden space-y-6">
            <!-- Intro Paragraph -->
            <div class="bg-white rounded-xl p-6 shadow-sm border border-slate-200">
                <h2 class="text-xl font-bold text-slate-900 mb-1">The Practical Standard & Question Construction</h2>
                <p class="text-slate-600 text-sm">
                    This section presents the standard verifier behavior framework across the three verification stages (Before, During, After), detailing the core <strong>Ask-Listen-Record</strong> evidence cycle. It also includes the interactive <strong>Guided Question Builder Tool</strong> for Activity 1, helping teams turn desktop review gaps into maximum 3 structured questions.
                </p>
            </div>

            <!-- Standard Framework: Before / During / After -->
            <div class="grid grid-cols-1 md:grid-cols-3 gap-4">
                <div class="bg-white p-5 rounded-xl border-t-4 border-amber-500 shadow-sm border-x border-b border-slate-200">
                    <div class="text-xs font-bold uppercase tracking-wider text-amber-700 mb-1">BEFORE INTERVIEW</div>
                    <h3 class="font-bold text-slate-900 text-base mb-2">Prepare Evidence Focus</h3>
                    <ul class="text-xs text-slate-600 space-y-2">
                        <li>• Review relevant VT requirement, verifier note & rating field.</li>
                        <li>• Compare SVR statement directly with reviewed evidence.</li>
                        <li>• State exactly what still needs checking during interview.</li>
                        <li>• Assign lead, supporting interviewer, rapporteur & timekeeper.</li>
                    </ul>
                </div>
                <div class="bg-white p-5 rounded-xl border-t-4 border-emerald-600 shadow-sm border-x border-b border-slate-200">
                    <div class="text-xs font-bold uppercase tracking-wider text-emerald-700 mb-1">DURING INTERVIEW</div>
                    <h3 class="font-bold text-slate-900 text-base mb-2">Ask, Listen & Check</h3>
                    <ul class="text-xs text-slate-600 space-y-2">
                        <li>• Explain purpose, roles, and available time clearly.</li>
                        <li>• Ask <strong>one clear question at a time</strong>.</li>
                        <li>• Listen fully; base follow-up directly on response.</li>
                        <li>• Request specific example or exact evidence source.</li>
                    </ul>
                </div>
                <div class="bg-white p-5 rounded-xl border-t-4 border-indigo-600 shadow-sm border-x border-b border-slate-200">
                    <div class="text-xs font-bold uppercase tracking-wider text-indigo-700 mb-1">AFTER INTERVIEW</div>
                    <h3 class="font-bold text-slate-900 text-base mb-2">Debrief & Triangulate</h3>
                    <ul class="text-xs text-slate-600 space-y-2">
                        <li>• Separate what was stated from evidence shown or identified.</li>
                        <li>• Compare notes and resolve recording differences.</li>
                        <li>• Identify contradictions, missing evidence or follow-up.</li>
                        <li>• <strong>Do not announce rating during interview!</strong></li>
                    </ul>
                </div>
            </div>

            <!-- Ask-Listen-Record Interactive Cards -->
            <div class="bg-slate-900 text-white rounded-xl p-6 shadow-md">
                <h3 class="text-base font-bold text-amber-400 mb-2">The Ask-Listen-Record Evidence Cycle</h3>
                <p class="text-xs text-slate-300 mb-4">Click each phase to see specific verifier execution habits.</p>
               
                <div class="grid grid-cols-1 md:grid-cols-3 gap-4">
                    <div class="bg-slate-800 border border-slate-700 rounded-lg p-4 hover:border-amber-500 transition cursor-pointer" onclick="toggleCycleDetail('ask')">
                        <div class="flex items-center justify-between mb-2">
                            <span class="text-xs font-bold text-amber-400 uppercase">Phase 1</span>
                            <span class="text-xl font-black text-slate-600">01</span>
                        </div>
                        <h4 class="text-base font-bold text-white mb-1">ASK</h4>
                        <p class="text-xs text-slate-300">Use "What must be checked" & "Who/evidence source" fields to frame one clear first question.</p>
                        <div id="cycle-ask" class="mt-3 pt-3 border-t border-slate-700 text-xs text-amber-200 space-y-1">
                            <p><strong>Rule:</strong> Avoid multi-part questions. Base directly on VT1-VT4/SVR priority.</p>
                        </div>
                    </div>

                    <div class="bg-slate-800 border border-slate-700 rounded-lg p-4 hover:border-emerald-500 transition cursor-pointer" onclick="toggleCycleDetail('listen')">
                        <div class="flex items-center justify-between mb-2">
                            <span class="text-xs font-bold text-emerald-400 uppercase">Phase 2</span>
                            <span class="text-xl font-black text-slate-600">02</span>
                        </div>
                        <h4 class="text-base font-bold text-white mb-1">LISTEN</h4>
                        <p class="text-xs text-slate-300">Allow response to guide next step. Ask for explanation, example, or record location only if answer needs support.</p>
                        <div id="cycle-listen" class="mt-3 pt-3 border-t border-slate-700 text-xs text-emerald-200 space-y-1">
                            <p><strong>Rule:</strong> Do not interrupt or coach the interviewee toward an answer.</p>
                        </div>
                    </div>

                    <div class="bg-slate-800 border border-slate-700 rounded-lg p-4 hover:border-indigo-500 transition cursor-pointer" onclick="toggleCycleDetail('record')">
                        <div class="flex items-center justify-between mb-2">
                            <span class="text-xs font-bold text-indigo-400 uppercase">Phase 3</span>
                            <span class="text-xl font-black text-slate-600">03</span>
                        </div>
                        <h4 class="text-base font-bold text-white mb-1">RECORD</h4>
                        <p class="text-xs text-slate-300">Link response to VT/SVR reference. Keep stakeholder claims separate from physical evidence shown.</p>
                        <div id="cycle-record" class="mt-3 pt-3 border-t border-slate-700 text-xs text-indigo-200 space-y-1">
                            <p><strong>Rule:</strong> Record statements, evidence, and verifier interpretations in distinct categories.</p>
                        </div>
                    </div>
                </div>
            </div>

            <!-- INTERACTIVE QUESTION BUILDER TOOL FOR ACTIVITY 1 -->
            <div class="bg-white rounded-xl p-6 shadow-sm border border-slate-200">
                <div class="flex flex-col md:flex-row md:items-center justify-between pb-4 mb-4 border-b border-slate-200 gap-2">
                    <div>
                        <span class="bg-amber-100 text-amber-800 text-xs font-bold px-2 py-0.5 rounded">Activity 1 Workspace</span>
                        <h3 class="text-lg font-bold text-slate-900 mt-1">Guided Question Builder (30-Minute Activity Tool)</h3>
                        <p class="text-xs text-slate-500">Turn one desktop-review matter into no more than 3 compliant interview questions.</p>
                    </div>
                    <button onclick="loadSampleQuestionSet()" class="text-xs bg-slate-800 hover:bg-slate-700 text-white font-semibold px-3 py-1.5 rounded transition">
                        Load Sample Desktop Priority
                    </button>
                </div>

                <div class="grid grid-cols-1 lg:grid-cols-12 gap-6">
                    <!-- Left: Form inputs for Question Construction -->
                    <div class="lg:col-span-7 space-y-4">
                        <div>
                            <label class="block text-xs font-bold text-slate-700 mb-1">1. Selected VT / SVR Priority Reference</label>
                            <input type="text" id="qb-ref" placeholder="e.g., VT4 Requirement 2.1 - Course Learning Outcome Attainment" class="w-full text-xs p-2.5 border border-slate-300 rounded focus:ring-2 focus:ring-amber-500 focus:outline-none">
                        </div>

                        <div>
                            <label class="block text-xs font-bold text-slate-700 mb-1">2. What Must Be Checked & Target Stakeholder</label>
                            <input type="text" id="qb-target" placeholder="e.g., Calculation worksheet for 82% outcome attainment (Programme Coordinator)" class="w-full text-xs p-2.5 border border-slate-300 rounded focus:ring-2 focus:ring-amber-500 focus:outline-none">
                        </div>

                        <!-- 3 Questions Generator Pattern -->
                        <div class="space-y-3 pt-2">
                            <h4 class="text-xs font-bold text-slate-800 uppercase tracking-wide">Draft Up To 3 Main Questions (Simple Pattern)</h4>
                           
                            <div class="bg-slate-50 p-3 rounded border border-slate-200">
                                <label class="block text-xs font-bold text-amber-800 mb-1">Question 1: Understand the Practice</label>
                                <input type="text" id="qb-q1" placeholder="e.g., Please explain how the reported 82% course learning outcome attainment result was calculated." class="w-full text-xs p-2 border border-slate-300 rounded focus:ring-1 focus:ring-amber-500">
                            </div>

                            <div class="bg-slate-50 p-3 rounded border border-slate-200">
                                <label class="block text-xs font-bold text-emerald-800 mb-1">Question 2: Obtain a Specific Example</label>
                                <input type="text" id="qb-q2" placeholder="e.g., Which specific assessment tasks and student cohorts were included in this calculation?" class="w-full text-xs p-2 border border-slate-300 rounded focus:ring-1 focus:ring-emerald-500">
                            </div>

                            <div class="bg-slate-50 p-3 rounded border border-slate-200">
                                <label class="block text-xs font-bold text-indigo-800 mb-1">Question 3: Identify Supporting Evidence</label>
                                <input type="text" id="qb-q3" placeholder="e.g., Which record or calculation worksheet can confirm this, and where can the team locate it?" class="w-full text-xs p-2 border border-slate-300 rounded focus:ring-1 focus:ring-indigo-500">
                            </div>
                        </div>

                        <div class="pt-2 flex gap-3">
                            <button onclick="run4QuestionChecks()" class="bg-amber-600 hover:bg-amber-700 text-white font-bold text-xs px-4 py-2 rounded shadow transition">
                                Apply 4-Check Validation
                            </button>
                            <button onclick="transferToAppendixA()" class="bg-slate-800 hover:bg-slate-900 text-white font-bold text-xs px-4 py-2 rounded shadow transition">
                                Send to Appendix A Planning Sheet
                            </button>
                        </div>
                    </div>

                    <!-- Right: 4 Quality Checks Validator Box -->
                    <div class="lg:col-span-5 bg-slate-50 p-4 rounded-xl border border-slate-200 flex flex-col justify-between">
                        <div>
                            <h4 class="text-xs font-bold text-slate-900 uppercase tracking-wide mb-3 flex items-center justify-between">
                                <span>Quality Checks Checklist</span>
                                <span class="text-[10px] bg-slate-200 text-slate-700 px-1.5 py-0.5 rounded">Activity 1 Standard</span>
                            </h4>

                            <div class="space-y-3 text-xs">
                                <div id="check-item-1" class="p-2.5 rounded bg-white border border-slate-200 flex items-start gap-2">
                                    <span class="check-icon font-bold text-slate-400">[ ]</span>
                                    <div>
                                        <p class="font-bold text-slate-800">1. Directly Linked to VT/SVR Priority</p>
                                        <p class="text-[11px] text-slate-500">Avoid general question lists; focus strictly on desktop review gap.</p>
                                    </div>
                                </div>

                                <div id="check-item-2" class="p-2.5 rounded bg-white border border-slate-200 flex items-start gap-2">
                                    <span class="check-icon font-bold text-slate-400">[ ]</span>
                                    <div>
                                        <p class="font-bold text-slate-800">2. Clear & Respectful Wording</p>
                                        <p class="text-[11px] text-slate-500">No leading questions, blaming language, or suggesting expected answers.</p>
                                    </div>
                                </div>

                                <div id="check-item-3" class="p-2.5 rounded bg-white border border-slate-200 flex items-start gap-2">
                                    <span class="check-icon font-bold text-slate-400">[ ]</span>
                                    <div>
                                        <p class="font-bold text-slate-800">3. Single Main Question at a Time</p>
                                        <p class="text-[11px] text-slate-500">Do not bundle several questions together into one paragraph.</p>
                                    </div>
                                </div>

                                <div id="check-item-4" class="p-2.5 rounded bg-white border border-slate-200 flex items-start gap-2">
                                    <span class="check-icon font-bold text-slate-400">[ ]</span>
                                    <div>
                                        <p class="font-bold text-slate-800">4. Can Produce Checkable Evidence</p>
                                        <p class="text-[11px] text-slate-500">Leads to an explanation, concrete example, or tangible document source.</p>
                                    </div>
                                </div>
                            </div>
                        </div>

                        <div id="validation-summary" class="mt-4 p-3 rounded bg-amber-50 text-amber-900 border border-amber-200 text-xs font-medium text-center">
                            Fill in your questions and click "Apply 4-Check Validation" above to test compliance.
                        </div>
                    </div>
                </div>
            </div>
        </section>


        <!-- ================= SECTION 3: TRAINER DEMONSTRATION ================= -->
        <section id="sec-demo" class="tab-content hidden space-y-6">
            <!-- Intro Paragraph -->
            <div class="bg-white rounded-xl p-6 shadow-sm border border-slate-200">
                <h2 class="text-xl font-bold text-slate-900 mb-1">Trainer Demonstration Module (09:15 - 09:30)</h2>
                <p class="text-slate-600 text-sm">
                    This 15-minute demonstration visually models the difference between a ineffective (weak) interview technique and an effective, evidence-focused approach before participants begin Activity 2. It includes a interactive reflection prompt at the mid-demonstration pause point.
                </p>
            </div>

            <!-- Scenario Setup Card -->
            <div class="bg-amber-900 text-amber-50 rounded-xl p-5 shadow-md">
                <div class="flex items-center justify-between mb-2">
                    <span class="text-xs font-bold uppercase tracking-wider text-amber-300">Demonstration Case Scenario</span>
                    <span class="text-xs bg-amber-800 px-2 py-1 rounded">SVR & VT4 Audit Focus</span>
                </div>
                <h3 class="text-base font-bold mb-1">Course Learning Outcome Attainment Gap</h3>
                <p class="text-xs text-amber-100 leading-relaxed">
                    <strong>SVR Statement:</strong> "82% of enrolled students achieved the prescribed course learning outcomes."<br>
                    <strong>Desktop Review Finding:</strong> The overall result is stated, but the underlying calculation worksheet, sample student grades, and record of review action were omitted from the submission.<br>
                    <strong>Verifier Task:</strong> Interview the Course Coordinator to check how the outcome was calculated, reviewed, and used to improve teaching.
                </p>
            </div>

            <!-- Side-by-Side Comparison Player -->
            <div class="grid grid-cols-1 md:grid-cols-2 gap-6">
                <!-- Weak Approach Block -->
                <div class="bg-red-50 rounded-xl p-5 border border-red-200 shadow-sm flex flex-col justify-between">
                    <div>
                        <div class="flex items-center justify-between mb-3">
                            <span class="text-xs font-bold text-red-700 uppercase bg-red-100 px-2 py-0.5 rounded">Weak Approach (3 Minutes)</span>
                            <span class="text-xs text-red-600 font-semibold">Avoid These Habits</span>
                        </div>
                       
                        <div class="space-y-3 text-xs text-slate-800">
                            <div class="bg-white p-3 rounded border border-red-200">
                                <p class="font-bold text-red-900 mb-1">Leading & Accusatory Question:</p>
                                <p class="italic text-slate-600">“Your evidence for attainment is incomplete, isn't it?”</p>
                            </div>
                            <div class="bg-white p-3 rounded border border-red-200">
                                <p class="font-bold text-red-900 mb-1">Multiple Bundled Questions:</p>
                                <p class="italic text-slate-600">“Did you calculate the 82% correctly, review it with colleagues, and make changes to improve teaching?”</p>
                            </div>
                            <div class="bg-white p-3 rounded border border-red-200">
                                <p class="font-bold text-red-900 mb-1">Blaming Language & Interruption:</p>
                                <p class="italic text-slate-600">“Why did you fail to attach the calculation worksheet?” <span class="text-red-600 font-bold">[Interrupts interviewee before they finish speaking]</span></p>
                            </div>
                        </div>
                    </div>
                    <div class="mt-4 pt-3 border-t border-red-200 text-[11px] text-red-800 font-medium">
                        <strong>Impact:</strong> Makes interviewee defensive, fails to locate actual evidence, and creates ambiguity.
                    </div>
                </div>

                <!-- Effective Approach Block -->
                <div class="bg-emerald-50 rounded-xl p-5 border border-emerald-200 shadow-sm flex flex-col justify-between">
                    <div>
                        <div class="flex items-center justify-between mb-3">
                            <span class="text-xs font-bold text-emerald-800 uppercase bg-emerald-100 px-2 py-0.5 rounded">Effective Approach (6 Minutes)</span>
                            <span class="text-xs text-emerald-700 font-semibold">Standard To Model</span>
                        </div>

                        <div class="space-y-2.5 text-xs text-slate-800">
                            <div class="bg-white p-2.5 rounded border border-emerald-200">
                                <p class="font-bold text-emerald-900">1. Professional Opening:</p>
                                <p class="text-slate-600">“We would like to understand how the reported outcome attainment was calculated and used. We have about 7 minutes for this topic.”</p>
                            </div>
                            <div class="bg-white p-2.5 rounded border border-emerald-200">
                                <p class="font-bold text-emerald-900">2. First Clear Question:</p>
                                <p class="text-slate-600">“Please explain how the 82% attainment result was calculated.”</p>
                            </div>
                            <div class="bg-white p-2.5 rounded border border-emerald-200">
                                <p class="font-bold text-emerald-900">3. Follow-up on Evidence Source:</p>
                                <p class="text-slate-600">“Which assessments were included, and could you identify the worksheet used?”</p>
                            </div>
                            <div class="bg-white p-2.5 rounded border border-emerald-200">
                                <p class="font-bold text-emerald-900">4. Factual Summary Closing:</p>
                                <p class="text-slate-600">“To confirm: the coordinator calculates the result using the assessment sheet, and actions are logged in meeting minutes. Is that accurate?”</p>
                            </div>
                        </div>
                    </div>
                    <div class="mt-4 pt-3 border-t border-emerald-200 text-[11px] text-emerald-900 font-medium">
                        <strong>Impact:</strong> Establishes clear factual record, identifies exact evidence location, keeps discussion professional.
                    </div>
                </div>
            </div>

            <!-- Mid-Demonstration Interactive Reflection Prompt -->
            <div class="bg-slate-800 text-white p-5 rounded-xl border border-slate-700 shadow-sm">
                <h3 class="text-sm font-bold text-amber-400 mb-2 flex items-center gap-2">
                    <span class="px-2 py-0.5 rounded bg-amber-500/20 text-amber-300 text-xs">Pause Point (Participant Reflection Prompt)</span>
                    What did you observe?
                </h3>
                <p class="text-xs text-slate-300 mb-4">When the trainer pauses during the demonstration, ask participants to identify:</p>
               
                <div class="grid grid-cols-1 md:grid-cols-3 gap-3">
                    <div class="bg-slate-900 p-3 rounded border border-slate-700 text-xs">
                        <span class="text-amber-400 font-bold block mb-1">1. What was heard?</span>
                        <p class="text-slate-400">The stakeholder explained that calculations happen in Excel, but moderation minutes are stored separately.</p>
                    </div>
                    <div class="bg-slate-900 p-3 rounded border border-slate-700 text-xs">
                        <span class="text-amber-400 font-bold block mb-1">2. What requires evidence?</span>
                        <p class="text-slate-400">The raw grade calculation sheet and the course committee meeting minutes reflecting the review.</p>
                    </div>
                    <div class="bg-slate-900 p-3 rounded border border-slate-700 text-xs">
                        <span class="text-amber-400 font-bold block mb-1">3. Next useful question?</span>
                        <p class="text-slate-400">“Where can the verifier team access the course committee meeting minutes for October?”</p>
                    </div>
                </div>
            </div>
        </section>


        <!-- ================= SECTION 4: PRACTICE & TIMER ================= -->
        <section id="sec-practice" class="tab-content hidden space-y-6">
            <!-- Intro Paragraph -->
            <div class="bg-white rounded-xl p-6 shadow-sm border border-slate-200">
                <h2 class="text-xl font-bold text-slate-900 mb-1">Activity 2: Coached Interview Practice Suite (09:30 - 10:15)</h2>
                <p class="text-slate-600 text-sm">
                    In this 45-minute coached practice, verifier teams conduct a complete practice interview using the priority and questions prepared in Activity 1. Use the interactive 5-person role assigner, live session stage clock, and digital Appendix B Observer Checklist below to manage the round.
                </p>
            </div>

            <!-- Team Roles Matrix (5 Persons) -->
            <div class="bg-white rounded-xl p-5 shadow-sm border border-slate-200">
                <h3 class="text-sm font-bold text-slate-900 mb-3">5-Person Team Role Assignment</h3>
                <div class="grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-5 gap-3">
                    <div class="p-3 bg-amber-50 rounded-lg border border-amber-200">
                        <span class="text-[10px] font-bold text-amber-800 uppercase block">Role 1</span>
                        <span class="font-bold text-slate-900 text-xs block mt-0.5">Lead Interviewer</span>
                        <p class="text-[11px] text-slate-600 mt-1">Leads opening, introduces team, asks Q1 and manages main sequence.</p>
                    </div>
                    <div class="p-3 bg-slate-50 rounded-lg border border-slate-200">
                        <span class="text-[10px] font-bold text-slate-600 uppercase block">Role 2</span>
                        <span class="font-bold text-slate-900 text-xs block mt-0.5">Supporting Interviewer</span>
                        <p class="text-[11px] text-slate-600 mt-1">Listens actively, asks follow-up on evidence or specific examples.</p>
                    </div>
                    <div class="p-3 bg-slate-50 rounded-lg border border-slate-200">
                        <span class="text-[10px] font-bold text-slate-600 uppercase block">Role 3</span>
                        <span class="text-[10px] font-bold text-indigo-700 uppercase block">Stakeholder</span>
                        <span class="font-bold text-slate-900 text-xs block mt-0.5">Programme Coordinator</span>
                        <p class="text-[11px] text-slate-600 mt-1">Answers from SVR/evidence only; does NOT invent unnecessary details.</p>
                    </div>
                    <div class="p-3 bg-slate-50 rounded-lg border border-slate-200">
                        <span class="text-[10px] font-bold text-slate-600 uppercase block">Role 4</span>
                        <span class="font-bold text-slate-900 text-xs block mt-0.5">Rapporteur</span>
                        <p class="text-[11px] text-slate-600 mt-1">Records key statements, evidence identified & unresolved gaps. Not transcript.</p>
                    </div>
                    <div class="p-3 bg-emerald-50 rounded-lg border border-emerald-200">
                        <span class="text-[10px] font-bold text-emerald-800 uppercase block">Role 5</span>
                        <span class="font-bold text-slate-900 text-xs block mt-0.5">Observer / Timekeeper</span>
                        <p class="text-[11px] text-slate-600 mt-1">Monitors time & completes Appendix B checklist for targeted feedback.</p>
                    </div>
                </div>
            </div>

            <!-- Practice Stage Timer & Allocation Chart -->
            <div class="grid grid-cols-1 lg:grid-cols-12 gap-6">
                <!-- Live Coached Session Timer -->
                <div class="lg:col-span-7 bg-slate-900 text-white rounded-xl p-6 shadow-md flex flex-col justify-between">
                    <div>
                        <div class="flex items-center justify-between border-b border-slate-700 pb-3 mb-4">
                            <div>
                                <span class="text-xs font-bold text-amber-400 uppercase tracking-wider">Activity 2 Live Clock</span>
                                <h3 class="text-lg font-bold text-white">45-Minute Coached Round Management</h3>
                            </div>
                            <span id="timer-stage-badge" class="bg-amber-500 text-slate-950 font-bold text-xs px-2.5 py-1 rounded">
                                Stage 1: Setup (5 min)
                            </span>
                        </div>

                        <div class="text-center py-4">
                            <div id="timer-display" class="text-5xl sm:text-6xl font-black font-mono tracking-tight text-white">
                                05:00
                            </div>
                            <p id="timer-stage-desc" class="text-xs text-amber-200 mt-2">
                                Confirm priority, 3 questions, stakeholder details, and team roles.
                            </p>
                        </div>

                        <!-- Phase Buttons -->
                        <div class="grid grid-cols-2 sm:grid-cols-5 gap-2 mt-4 text-[11px]">
                            <button onclick="setTimerPhase(1)" class="p-2 bg-slate-800 hover:bg-slate-700 rounded border border-slate-700 text-center text-slate-300 font-semibold focus:border-amber-400">
                                1. Setup (5m)
                            </button>
                            <button onclick="setTimerPhase(2)" class="p-2 bg-slate-800 hover:bg-slate-700 rounded border border-slate-700 text-center text-slate-300 font-semibold focus:border-amber-400">
                                2. Interview (15m)
                            </button>
                            <button onclick="setTimerPhase(3)" class="p-2 bg-slate-800 hover:bg-slate-700 rounded border border-slate-700 text-center text-slate-300 font-semibold focus:border-amber-400">
                                3. Debrief (10m)
                            </button>
                            <button onclick="setTimerPhase(4)" class="p-2 bg-slate-800 hover:bg-slate-700 rounded border border-slate-700 text-center text-slate-300 font-semibold focus:border-amber-400">
                                4. Coaching (10m)
                            </button>
                            <button onclick="setTimerPhase(5)" class="p-2 bg-slate-800 hover:bg-slate-700 rounded border border-slate-700 text-center text-slate-300 font-semibold focus:border-amber-400">
                                5. Record (5m)
                            </button>
                        </div>
                    </div>

                    <div class="flex items-center justify-center gap-3 mt-6 pt-4 border-t border-slate-800">
                        <button id="btn-start-timer" onclick="startTimer()" class="bg-amber-500 hover:bg-amber-600 text-slate-950 font-bold text-xs px-6 py-2.5 rounded transition shadow">
                            Start Stage Timer
                        </button>
                        <button onclick="pauseTimer()" class="bg-slate-800 hover:bg-slate-700 text-slate-200 font-bold text-xs px-4 py-2.5 rounded border border-slate-700 transition">
                            Pause
                        </button>
                        <button onclick="resetTimer()" class="bg-slate-800 hover:bg-slate-700 text-slate-400 font-bold text-xs px-4 py-2.5 rounded border border-slate-700 transition">
                            Reset
                        </button>
                    </div>
                </div>

                <!-- 45-Min Allocation Chart -->
                <div class="lg:col-span-5 bg-white rounded-xl p-5 shadow-sm border border-slate-200">
                    <h3 class="text-sm font-bold text-slate-900 mb-2">45-Minute Coached Round Allocation</h3>
                    <div class="chart-container">
                        <canvas id="practiceChart"></canvas>
                    </div>
                </div>
            </div>

            <!-- APPENDIX B: INTERACTIVE OBSERVER CHECKLIST -->
            <div class="bg-white rounded-xl p-6 shadow-sm border border-slate-200">
                <div class="flex flex-col md:flex-row md:items-center justify-between pb-4 mb-4 border-b border-slate-200 gap-2">
                    <div>
                        <span class="bg-emerald-100 text-emerald-800 text-xs font-bold px-2 py-0.5 rounded">Appendix B Tool</span>
                        <h3 class="text-lg font-bold text-slate-900 mt-1">Interview Practice Observer Checklist</h3>
                        <p class="text-xs text-slate-500">Completed by Timekeeper/Observer during Activity 2 round.</p>
                    </div>
                    <div class="text-xs bg-slate-100 px-3 py-1.5 rounded font-mono text-slate-700">
                        Observed Score: <span id="obs-score-count" class="font-bold text-emerald-700">0 / 10 Yes</span>
                    </div>
                </div>

                <div class="overflow-x-auto custom-scrollbar">
                    <table class="w-full text-left text-xs">
                        <thead class="bg-slate-100 text-slate-800 font-bold uppercase text-[11px]">
                            <tr>
                                <th class="p-3 w-7/12">Observed Behavior Standard</th>
                                <th class="p-3 w-3/12 text-center">Rating</th>
                                <th class="p-3 w-2/12">Short Note</th>
                            </tr>
                        </thead>
                        <tbody class="divide-y divide-slate-100 text-slate-700">
                            <!-- Items 1 to 10 -->
                            <tr>
                                <td class="p-3 font-medium">1. Explained purpose, stakeholder group, team roles & available time.</td>
                                <td class="p-3 text-center">
                                    <select onchange="updateObsScore()" class="obs-rate text-xs p-1 border rounded bg-slate-50">
                                        <option value="No">No</option>
                                        <option value="Partly">Partly</option>
                                        <option value="Yes" selected>Yes</option>
                                    </select>
                                </td>
                                <td class="p-3"><input type="text" placeholder="Note..." class="w-full text-xs p-1 border rounded"></td>
                            </tr>
                            <tr>
                                <td class="p-3 font-medium">2. Main question linked directly to specific VT1-VT4/SVR priority.</td>
                                <td class="p-3 text-center">
                                    <select onchange="updateObsScore()" class="obs-rate text-xs p-1 border rounded bg-slate-50">
                                        <option value="No">No</option>
                                        <option value="Partly">Partly</option>
                                        <option value="Yes" selected>Yes</option>
                                    </select>
                                </td>
                                <td class="p-3"><input type="text" placeholder="Note..." class="w-full text-xs p-1 border rounded"></td>
                            </tr>
                            <tr>
                                <td class="p-3 font-medium">3. Asked one clear question at a time (no bundling).</td>
                                <td class="p-3 text-center">
                                    <select onchange="updateObsScore()" class="obs-rate text-xs p-1 border rounded bg-slate-50">
                                        <option value="No">No</option>
                                        <option value="Partly">Partly</option>
                                        <option value="Yes">Yes</option>
                                    </select>
                                </td>
                                <td class="p-3"><input type="text" placeholder="Note..." class="w-full text-xs p-1 border rounded"></td>
                            </tr>
                            <tr>
                                <td class="p-3 font-medium">4. Listened actively without interrupting, arguing or coaching answer.</td>
                                <td class="p-3 text-center">
                                    <select onchange="updateObsScore()" class="obs-rate text-xs p-1 border rounded bg-slate-50">
                                        <option value="No">No</option>
                                        <option value="Partly">Partly</option>
                                        <option value="Yes" selected>Yes</option>
                                    </select>
                                </td>
                                <td class="p-3"><input type="text" placeholder="Note..." class="w-full text-xs p-1 border rounded"></td>
                            </tr>
                            <tr>
                                <td class="p-3 font-medium">5. Follow-up questions were based on actual response received.</td>
                                <td class="p-3 text-center">
                                    <select onchange="updateObsScore()" class="obs-rate text-xs p-1 border rounded bg-slate-50">
                                        <option value="No">No</option>
                                        <option value="Partly">Partly</option>
                                        <option value="Yes">Yes</option>
                                    </select>
                                </td>
                                <td class="p-3"><input type="text" placeholder="Note..." class="w-full text-xs p-1 border rounded"></td>
                            </tr>
                            <tr>
                                <td class="p-3 font-medium">6. Requested specific example or exact evidence source when needed.</td>
                                <td class="p-3 text-center">
                                    <select onchange="updateObsScore()" class="obs-rate text-xs p-1 border rounded bg-slate-50">
                                        <option value="No">No</option>
                                        <option value="Partly">Partly</option>
                                        <option value="Yes">Yes</option>
                                    </select>
                                </td>
                                <td class="p-3"><input type="text" placeholder="Note..." class="w-full text-xs p-1 border rounded"></td>
                            </tr>
                            <tr>
                                <td class="p-3 font-medium">7. Rapporteur separated stakeholder response, evidence shown & note.</td>
                                <td class="p-3 text-center">
                                    <select onchange="updateObsScore()" class="obs-rate text-xs p-1 border rounded bg-slate-50">
                                        <option value="No">No</option>
                                        <option value="Partly">Partly</option>
                                        <option value="Yes">Yes</option>
                                    </select>
                                </td>
                                <td class="p-3"><input type="text" placeholder="Note..." class="w-full text-xs p-1 border rounded"></td>
                            </tr>
                            <tr>
                                <td class="p-3 font-medium">8. Participation and time were managed appropriately within limits.</td>
                                <td class="p-3 text-center">
                                    <select onchange="updateObsScore()" class="obs-rate text-xs p-1 border rounded bg-slate-50">
                                        <option value="No">No</option>
                                        <option value="Partly">Partly</option>
                                        <option value="Yes">Yes</option>
                                    </select>
                                </td>
                                <td class="p-3"><input type="text" placeholder="Note..." class="w-full text-xs p-1 border rounded"></td>
                            </tr>
                            <tr>
                                <td class="p-3 font-medium">9. Summarised factual understanding and invited stakeholder correction.</td>
                                <td class="p-3 text-center">
                                    <select onchange="updateObsScore()" class="obs-rate text-xs p-1 border rounded bg-slate-50">
                                        <option value="No">No</option>
                                        <option value="Partly">Partly</option>
                                        <option value="Yes">Yes</option>
                                    </select>
                                </td>
                                <td class="p-3"><input type="text" placeholder="Note..." class="w-full text-xs p-1 border rounded"></td>
                            </tr>
                            <tr>
                                <td class="p-3 font-medium">10. Closed professionally and did NOT announce rating or decision.</td>
                                <td class="p-3 text-center">
                                    <select onchange="updateObsScore()" class="obs-rate text-xs p-1 border rounded bg-slate-50">
                                        <option value="No">No</option>
                                        <option value="Partly">Partly</option>
                                        <option value="Yes" selected>Yes</option>
                                    </select>
                                </td>
                                <td class="p-3"><input type="text" placeholder="Note..." class="w-full text-xs p-1 border rounded"></td>
                            </tr>
                        </tbody>
                    </table>
                </div>

                <!-- Structured Feedback Formula Input -->
                <div class="mt-6 pt-4 border-t border-slate-200 bg-slate-50 p-4 rounded-lg">
                    <h4 class="text-xs font-bold text-slate-800 uppercase tracking-wide mb-2">3-Part Focused Feedback Formula</h4>
                    <div class="grid grid-cols-1 md:grid-cols-3 gap-3 text-xs">
                        <div>
                            <label class="block font-bold text-emerald-800 mb-1">1. One Strength (What helped):</label>
                            <input type="text" placeholder="e.g., Lead interviewer kept questions clearly linked to SVR priority." class="w-full p-2 border rounded border-slate-300">
                        </div>
                        <div>
                            <label class="block font-bold text-amber-800 mb-1">2. One Improvement (Reduced clarity):</label>
                            <input type="text" placeholder="e.g., Supporting interviewer asked two questions joined together." class="w-full p-2 border rounded border-slate-300">
                        </div>
                        <div>
                            <label class="block font-bold text-indigo-800 mb-1">3. One Action (For next round):</label>
                            <input type="text" placeholder="e.g., Pause after the answer before framing the follow-up prompt." class="w-full p-2 border rounded border-slate-300">
                        </div>
                    </div>
                </div>
            </div>
        </section>


        <!-- ================= SECTION 5: REFERENCE TOOLKIT ================= -->
        <section id="sec-toolkit" class="tab-content hidden space-y-6">
            <!-- Intro Paragraph -->
            <div class="bg-white rounded-xl p-6 shadow-sm border border-slate-200">
                <h2 class="text-xl font-bold text-slate-900 mb-1">Practical Interview Reference Toolkit</h2>
                <p class="text-slate-600 text-sm">
                    A quick-reference guide during interview preparation and facilitator feedback. Explore essential Do's and Don'ts across all 7 interview stages, or use the interactive decision matrix below to handle challenging interview situations effectively.
                </p>
            </div>

            <!-- Do's and Don'ts Filterable Table -->
            <div class="bg-white rounded-xl p-6 shadow-sm border border-slate-200">
                <div class="flex flex-col sm:flex-row sm:items-center justify-between gap-3 mb-4">
                    <h3 class="text-base font-bold text-slate-900">Stage-by-Stage Do's and Don'ts Reference</h3>
                    <div class="flex items-center gap-2">
                        <label class="text-xs font-semibold text-slate-500">Filter Stage:</label>
                        <select id="toolkit-stage-filter" onchange="filterToolkitStage(this.value)" class="text-xs p-1.5 border border-slate-300 rounded font-semibold text-slate-700">
                            <option value="all">All 7 Stages</option>
                            <option value="Prepare">1. Prepare</option>
                            <option value="Open">2. Open</option>
                            <option value="Ask">3. Ask</option>
                            <option value="Listen">4. Listen</option>
                            <option value="Evidence">5. Evidence Focus</option>
                            <option value="Record">6. Record</option>
                            <option value="Close">7. Close</option>
                        </select>
                    </div>
                </div>

                <div class="overflow-x-auto custom-scrollbar">
                    <table class="w-full text-left text-xs">
                        <thead class="bg-slate-100 text-slate-800 font-bold uppercase text-[11px]">
                            <tr>
                                <th class="p-3 w-2/12">Stage</th>
                                <th class="p-3 w-5/12 text-emerald-900 bg-emerald-50/50">DO (Effective Practice)</th>
                                <th class="p-3 w-5/12 text-red-900 bg-red-50/50">AVOID (Weak Habit)</th>
                            </tr>
                        </thead>
                        <tbody id="toolkit-table-body" class="divide-y divide-slate-100 text-slate-700">
                            <tr data-stage="Prepare">
                                <td class="p-3 font-bold text-slate-900">Prepare</td>
                                <td class="p-3 bg-emerald-50/20">Review VT/SVR reference, evidence gap, and select appropriate stakeholder.</td>
                                <td class="p-3 bg-red-50/20">Preparing a long general question list or asking every standard guiding question.</td>
                            </tr>
                            <tr data-stage="Open">
                                <td class="p-3 font-bold text-slate-900">Open</td>
                                <td class="p-3 bg-emerald-50/20">Explain purpose, roles, available time, and how information will be used.</td>
                                <td class="p-3 bg-red-50/20">Beginning abruptly or promising confidentiality beyond agreed verification rules.</td>
                            </tr>
                            <tr data-stage="Ask">
                                <td class="p-3 font-bold text-slate-900">Ask</td>
                                <td class="p-3 bg-emerald-50/20">Use one clear, respectful question linked to what must be checked.</td>
                                <td class="p-3 bg-red-50/20">Leading, blaming, vague, or several questions joined together.</td>
                            </tr>
                            <tr data-stage="Listen">
                                <td class="p-3 font-bold text-slate-900">Listen</td>
                                <td class="p-3 bg-emerald-50/20">Allow response to finish and invite relevant participants to contribute.</td>
                                <td class="p-3 bg-red-50/20">Interrupting, arguing, coaching the answer, or letting one person dominate.</td>
                            </tr>
                            <tr data-stage="Evidence">
                                <td class="p-3 font-bold text-slate-900">Evidence</td>
                                <td class="p-3 bg-emerald-50/20">Ask for a specific example or exact evidence source when needed.</td>
                                <td class="p-3 bg-red-50/20">Treating a stakeholder statement as sufficient proof without checking records.</td>
                            </tr>
                            <tr data-stage="Record">
                                <td class="p-3 font-bold text-slate-900">Record</td>
                                <td class="p-3 bg-emerald-50/20">Separate what was stated, evidence shown, verifier note, and follow-up.</td>
                                <td class="p-3 bg-red-50/20">Writing full transcript, unnecessary personal data, or unsupported conclusions.</td>
                            </tr>
                            <tr data-stage="Close">
                                <td class="p-3 font-bold text-slate-900">Close</td>
                                <td class="p-3 bg-emerald-50/20">Summarise factual understanding, invite correction, and explain next step.</td>
                                <td class="p-3 bg-red-50/20">Announcing a rating, finding, or approval decision during interview.</td>
                            </tr>
                        </tbody>
                    </table>
                </div>
            </div>

            <!-- Handling Difficult Interview Situations Matrix -->
            <div class="bg-white rounded-xl p-6 shadow-sm border border-slate-200">
                <h3 class="text-base font-bold text-slate-900 mb-1">When the Interview Becomes Difficult</h3>
                <p class="text-xs text-slate-500 mb-4">Click any situation to highlight recommended verifier response strategy.</p>

                <div class="grid grid-cols-1 md:grid-cols-2 gap-4">
                    <div class="p-4 rounded-lg bg-slate-50 border border-slate-200 hover:border-amber-500 transition cursor-pointer" onclick="highlightDiffScenario(this)">
                        <div class="flex items-center justify-between mb-1">
                            <span class="text-xs font-bold text-amber-800">Situation 1</span>
                            <span class="text-[10px] bg-slate-200 px-2 py-0.5 rounded text-slate-700">Vague Response</span>
                        </div>
                        <h4 class="text-xs font-bold text-slate-900 mb-2">Stakeholder provides a high-level or general answer.</h4>
                        <div class="text-xs text-slate-600 bg-white p-2.5 rounded border border-slate-200">
                            <strong>Recommended Response:</strong> “Can you give one specific recent example, and identify which record confirms it?”
                        </div>
                    </div>

                    <div class="p-4 rounded-lg bg-slate-50 border border-slate-200 hover:border-amber-500 transition cursor-pointer" onclick="highlightDiffScenario(this)">
                        <div class="flex items-center justify-between mb-1">
                            <span class="text-xs font-bold text-amber-800">Situation 2</span>
                            <span class="text-[10px] bg-slate-200 px-2 py-0.5 rounded text-slate-700">Overly Long Answer</span>
                        </div>
                        <h4 class="text-xs font-bold text-slate-900 mb-2">Stakeholder speaks at length off-topic.</h4>
                        <div class="text-xs text-slate-600 bg-white p-2.5 rounded border border-slate-200">
                            <strong>Recommended Response:</strong> Thank the stakeholder, politely restate the exact matter being checked, and ask the next focused question.
                        </div>
                    </div>

                    <div class="p-4 rounded-lg bg-slate-50 border border-slate-200 hover:border-amber-500 transition cursor-pointer" onclick="highlightDiffScenario(this)">
                        <div class="flex items-center justify-between mb-1">
                            <span class="text-xs font-bold text-amber-800">Situation 3</span>
                            <span class="text-[10px] bg-slate-200 px-2 py-0.5 rounded text-slate-700">Unknown Information</span>
                        </div>
                        <h4 class="text-xs font-bold text-slate-900 mb-2">Stakeholder does not know the answer.</h4>
                        <div class="text-xs text-slate-600 bg-white p-2.5 rounded border border-slate-200">
                            <strong>Recommended Response:</strong> Do not pressure the person. Record who or which specific document can provide the required information.
                        </div>
                    </div>

                    <div class="p-4 rounded-lg bg-slate-50 border border-slate-200 hover:border-amber-500 transition cursor-pointer" onclick="highlightDiffScenario(this)">
                        <div class="flex items-center justify-between mb-1">
                            <span class="text-xs font-bold text-amber-800">Situation 4</span>
                            <span class="text-[10px] bg-slate-200 px-2 py-0.5 rounded text-slate-700">Defensive Behavior</span>
                        </div>
                        <h4 class="text-xs font-bold text-slate-900 mb-2">Stakeholder becomes defensive or anxious.</h4>
                        <div class="text-xs text-slate-600 bg-white p-2.5 rounded border border-slate-200">
                            <strong>Recommended Response:</strong> Restate that the purpose is to understand and verify programme evidence, not to blame individuals.
                        </div>
                    </div>
                </div>

                <!-- Professional Safeguard Notice -->
                <div class="mt-4 p-3 rounded-lg bg-amber-50 border border-amber-200 text-xs text-amber-900 flex items-center gap-2">
                    <span class="font-bold text-amber-800">Professional Safeguard:</span>
                    <span>Declare any conflict of interest to facilitator immediately, discuss only information relevant to verification, and keep all notes in official records.</span>
                </div>
            </div>
        </section>


        <!-- ================= SECTION 6: APPENDICES & MOCK PREP ================= -->
        <section id="sec-appendices" class="tab-content hidden space-y-6">
            <!-- Intro Paragraph -->
            <div class="bg-white rounded-xl p-6 shadow-sm border border-slate-200">
                <h2 class="text-xl font-bold text-slate-900 mb-1">Mock Interview Preparation & Post-Session Tools</h2>
                <p class="text-slate-600 text-sm">
                    In the final 15 minutes (10:15–10:30), teams complete the 5-point readiness check, set up their official Appendix A planning sheet, and review the 4-part post-interview evidence debrief process.
                </p>
            </div>

            <!-- Readiness Checklist (10:15 - 10:30) -->
            <div class="bg-white rounded-xl p-6 shadow-sm border border-slate-200">
                <div class="flex items-center justify-between border-b border-slate-200 pb-3 mb-4">
                    <h3 class="text-base font-bold text-slate-900">5-Minute Readiness Check for Mock Session</h3>
                    <span id="readiness-counter" class="text-xs bg-slate-100 text-slate-700 px-2.5 py-1 rounded font-bold">0 of 5 Ready</span>
                </div>

                <div class="space-y-3 text-xs">
                    <label class="flex items-start gap-3 p-3 bg-slate-50 rounded border border-slate-200 cursor-pointer hover:bg-amber-50/50 transition">
                        <input type="checkbox" onchange="updateReadinessCount()" class="ready-chk mt-0.5 rounded text-amber-600 focus:ring-amber-500">
                        <div>
                            <span class="font-bold text-slate-900 block">1. Evidence Focus Ready</span>
                            <span class="text-slate-500">Every main question is linked directly to a stated VT1-VT4 or SVR priority matter.</span>
                        </div>
                    </label>

                    <label class="flex items-start gap-3 p-3 bg-slate-50 rounded border border-slate-200 cursor-pointer hover:bg-amber-50/50 transition">
                        <input type="checkbox" onchange="updateReadinessCount()" class="ready-chk mt-0.5 rounded text-amber-600 focus:ring-amber-500">
                        <div>
                            <span class="font-bold text-slate-900 block">2. Team Roles Assigned</span>
                            <span class="text-slate-500">Lead interviewer, supporting interviewer(s), rapporteur, and timekeeper are clearly confirmed.</span>
                        </div>
                    </label>

                    <label class="flex items-start gap-3 p-3 bg-slate-50 rounded border border-slate-200 cursor-pointer hover:bg-amber-50/50 transition">
                        <input type="checkbox" onchange="updateReadinessCount()" class="ready-chk mt-0.5 rounded text-amber-600 focus:ring-amber-500">
                        <div>
                            <span class="font-bold text-slate-900 block">3. Maximum 3 Questions Formulated</span>
                            <span class="text-slate-500">First question is clear; follow-up prompts are flexible based on interviewee response.</span>
                        </div>
                    </label>

                    <label class="flex items-start gap-3 p-3 bg-slate-50 rounded border border-slate-200 cursor-pointer hover:bg-amber-50/50 transition">
                        <input type="checkbox" onchange="updateReadinessCount()" class="ready-chk mt-0.5 rounded text-amber-600 focus:ring-amber-500">
                        <div>
                            <span class="font-bold text-slate-900 block">4. Desktop Records Open</span>
                            <span class="text-slate-500">VT1-VT4, SVR, and priority desktop review records are accessible to team members.</span>
                        </div>
                    </label>

                    <label class="flex items-start gap-3 p-3 bg-slate-50 rounded border border-slate-200 cursor-pointer hover:bg-amber-50/50 transition">
                        <input type="checkbox" onchange="updateReadinessCount()" class="ready-chk mt-0.5 rounded text-amber-600 focus:ring-amber-500">
                        <div>
                            <span class="font-bold text-slate-900 block">5. Timing & Conduct Agreed</span>
                            <span class="text-slate-500">Opening, interview, summary, and closing times confirmed. Team agrees NOT to announce ratings.</span>
                        </div>
                    </label>
                </div>
            </div>

            <!-- Post-Interview Debrief 4 Information Types -->
            <div class="bg-slate-900 text-white rounded-xl p-6 shadow-md">
                <h3 class="text-base font-bold text-amber-400 mb-1">Post-Interview Debrief & Information Separation</h3>
                <p class="text-xs text-slate-300 mb-4">Immediately following each session, teams must separate notes into 4 distinct categories before triangulation.</p>

                <div class="grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-4 gap-3 text-xs">
                    <div class="bg-slate-800 p-3.5 rounded border border-slate-700">
                        <span class="text-amber-400 font-bold block mb-1">1. Stakeholder Response</span>
                        <p class="text-slate-300">What the participant verbally explained or stated during the interview.</p>
                    </div>
                    <div class="bg-slate-800 p-3.5 rounded border border-slate-700">
                        <span class="text-emerald-400 font-bold block mb-1">2. Evidence Shown</span>
                        <p class="text-slate-300">Exact document, section, system record, or file named or physically inspected.</p>
                    </div>
                    <div class="bg-slate-800 p-3.5 rounded border border-slate-700">
                        <span class="text-indigo-400 font-bold block mb-1">3. Verifier Note</span>
                        <p class="text-slate-300">Team analysis on relevance to VT/SVR matter, including gaps identified.</p>
                    </div>
                    <div class="bg-slate-800 p-3.5 rounded border border-slate-700">
                        <span class="text-rose-400 font-bold block mb-1">4. Follow-up Action</span>
                        <p class="text-slate-300">What still requires checking, responsible person, and triangulation plan.</p>
                    </div>
                </div>
            </div>

            <!-- APPENDIX A FORM GENERATOR -->
            <div id="appendix-a-container" class="bg-white rounded-xl p-6 shadow-sm border border-slate-200">
                <div class="flex flex-col sm:flex-row sm:items-center justify-between border-b border-slate-200 pb-3 mb-4 gap-2">
                    <div>
                        <span class="bg-amber-100 text-amber-800 text-xs font-bold px-2 py-0.5 rounded">Appendix A Form</span>
                        <h3 class="text-lg font-bold text-slate-900 mt-1">Stakeholder Interview Planning Sheet</h3>
                        <p class="text-xs text-slate-500">Record max 3 main priorities for the mock interview session.</p>
                    </div>
                    <button onclick="window.print()" class="text-xs bg-slate-800 text-white font-bold px-3 py-1.5 rounded hover:bg-slate-700 transition">
                        Print / Export Sheet
                    </button>
                </div>

                <div class="space-y-4 text-xs">
                    <!-- Top Metadata -->
                    <div class="grid grid-cols-1 sm:grid-cols-2 gap-3">
                        <div>
                            <label class="block font-bold text-slate-700 mb-1">Programme / Assigned SVR:</label>
                            <input type="text" id="app-a-prog" placeholder="e.g., Bachelor of Computer Science SVR 2026" class="w-full p-2 border rounded">
                        </div>
                        <div>
                            <label class="block font-bold text-slate-700 mb-1">Verifier Team / Stakeholder Session:</lab
