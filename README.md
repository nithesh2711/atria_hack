🚨 Project: CrisisSync AI

Real-time AI-powered emergency coordination platform for hospitality

🎯 Core Value Proposition (Pitch-Ready)

CrisisSync AI acts as a central command system that:

Detects emergencies using AI
Instantly alerts all stakeholders
Guides safe evacuation in real time

Unlike traditional systems, it unifies guests, staff, and responders in one live network.

🧠 Elevator Pitch (30–40 sec)

“Hospitality venues struggle with fragmented communication during emergencies. CrisisSync AI solves this by combining AI detection, real-time alerts, and intelligent evacuation guidance into a single platform. It transforms chaotic crisis response into a coordinated, data-driven system that can save lives.”

🏗️ Repo Structure (Production-Oriented)
crisis-sync-ai/
│
├── client/                     # Frontend (Next.js)
│   ├── app/
│   │   ├── dashboard/         # Admin dashboard
│   │   ├── guest/             # Guest emergency UI
│   │   ├── staff/             # Staff control panel
│   │   └── layout.tsx
│   ├── components/
│   │   ├── AlertCard.tsx
│   │   ├── MapView.tsx
│   │   ├── EmergencyButton.tsx
│   │   └── VoiceInput.tsx
│   ├── lib/
│   │   └── supabaseClient.ts
│   └── styles/
│
├── server/                    # Backend APIs
│   ├── routes/
│   │   ├── alertRoutes.js
│   │   ├── aiRoutes.js
│   │   └── userRoutes.js
│   ├── services/
│   │   ├── aiDetection.js
│   │   ├── notificationService.js
│   │   └── routingEngine.js
│   └── index.js
│
├── ai-engine/                 # AI models
│   ├── vision/
│   │   └── yolo_detection.py
│   ├── audio/
│   │   └── anomaly_detection.py
│   └── nlp/
│       └── incident_classifier.py
│
├── supabase/
│   ├── migrations/
│   └── seed.sql
│
├── .env.example
├── README.md
└── package.json
🧩 Core Features (Hackathon Scope)
1. Emergency Trigger System
One-tap SOS button
Voice-triggered emergency detection

Tech:

Supabase (real-time DB)
Firebase Cloud Messaging
2. AI Incident Classifier
Input: voice/text (“fire in kitchen”)
Output: category + severity

Tech:

OpenAI API (LLM classification)
3. Live Alert Broadcasting
Alerts instantly visible to:
Staff dashboard
Guests
Color-coded severity system
4. Smart Evacuation Map
Shows:
Safe exits
Blocked paths
(Basic version: static map + dynamic markers)
5. Role-Based Interfaces
Guest: SOS + guidance
Staff: Assign tasks
Admin: Full control dashboard
📱 UI Screens (Design Blueprint)
1. Guest App
Big “EMERGENCY BUTTON”
Voice input (“Report incident”)
Live instructions:
“Move to Exit A”
“Avoid corridor B”
2. Staff Panel
Active incidents list
Assignable tasks:
“Check Room 204”
“Assist evacuation”
Status toggles (Done / In Progress)
3. Admin Dashboard (Main Demo Screen)
Real-time map
Incident timeline
Alerts panel
System status (green/yellow/red)
4. Incident Detail View
Type: Fire / Medical / Security
Location
AI-generated action plan
⚙️ Implementation Flow
Step 1: Setup Backend
Create project in Supabase
Tables:
users
incidents
alerts
locations
Step 2: Realtime Sync
Use Supabase subscriptions:
supabase
  .channel('alerts')
  .on('postgres_changes', { event: 'INSERT', schema: 'public', table: 'alerts' }, handler)
  .subscribe()
Step 3: AI Integration
Send incident text → OpenAI API
Return:
type
severity
recommended actions
Step 4: Notifications
Trigger push using Firebase
Also update UI in real time
Step 5: Map + Routing (Simplified)
Use static floor plan image
Overlay markers for:
hazards
exits
🔥 Demo Scenario (Very Important)

Simulate this in hackathon:

Click “Fire in Kitchen”
AI classifies → HIGH severity
Alert sent instantly
Dashboard updates live
Guest screen shows evacuation route

👉 This flow wins demos.

🚀 Advanced Add-ons (If Time Permits)
CCTV detection using YOLO
Voice input using Whisper
Predictive alerts (crowd density)
💡 Judging Points You’ll Hit
Innovation: AI + real-time coordination
Impact: Life-saving use case
Technical depth: Full-stack + AI
Scalability: Multi-property support
🧾 README Key Sections

Include:

Problem statement
Architecture diagram
Demo video link
Setup instructions
Future scope
🧠 One Strategic Tip

Don’t try to build everything.
Focus on:

Real-time alerts
AI classification
Clean UI demo
