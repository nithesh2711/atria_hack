# CrisisSync AI — Frontend Implementation
## Rapid Crisis Response Platform for Hospitality

> **Stack**: React 18 + Vite + Tailwind CSS v3 + React Router v6 + Framer Motion + Recharts + Lucide React  
> **Mode**: Dark-mode, emergency-grade UI — NOC (Network Operations Center) aesthetic  
> **Cursor Studio**: All files ready to copy into a Vite project

---

## Project Structure

```
crisisync-ai/
├── public/
│   └── vite.svg
├── src/
│   ├── assets/
│   ├── components/
│   │   ├── layout/
│   │   │   ├── Sidebar.jsx
│   │   │   ├── Header.jsx
│   │   │   └── RightPanel.jsx
│   │   ├── dashboard/
│   │   │   ├── IncidentCard.jsx
│   │   │   ├── SensorStatus.jsx
│   │   │   ├── PropertyMap.jsx
│   │   │   ├── EvacuationProgress.jsx
│   │   │   ├── StaffTracker.jsx
│   │   │   └── AlertsBroadcast.jsx
│   │   ├── modals/
│   │   │   ├── BroadcastModal.jsx
│   │   │   ├── EscalateModal.jsx
│   │   │   └── IncidentDetailModal.jsx
│   │   └── ui/
│   │       ├── SOSButton.jsx
│   │       ├── StatusBadge.jsx
│   │       ├── PulsingDot.jsx
│   │       └── AnimatedCounter.jsx
│   ├── pages/
│   │   ├── Login.jsx
│   │   ├── Dashboard.jsx
│   │   ├── IncidentLog.jsx
│   │   ├── DigitalTwin.jsx
│   │   ├── VoiceAssistant.jsx
│   │   └── Reports.jsx
│   ├── data/
│   │   ├── incidents.js
│   │   ├── sensors.js
│   │   ├── staff.js
│   │   └── mapData.js
│   ├── hooks/
│   │   ├── useIncidentFeed.js
│   │   ├── useSensorStream.js
│   │   └── useVoiceDetection.js
│   ├── context/
│   │   └── CrisisContext.jsx
│   ├── App.jsx
│   ├── main.jsx
│   └── index.css
├── index.html
├── vite.config.js
├── tailwind.config.js
└── package.json
```

---

## 1. Setup Files

### `package.json`

```json
{
  "name": "crisisync-ai",
  "private": true,
  "version": "1.0.0",
  "type": "module",
  "scripts": {
    "dev": "vite",
    "build": "vite build",
    "preview": "vite preview"
  },
  "dependencies": {
    "react": "^18.3.1",
    "react-dom": "^18.3.1",
    "react-router-dom": "^6.26.2",
    "framer-motion": "^11.5.4",
    "lucide-react": "^0.446.0",
    "recharts": "^2.12.7",
    "clsx": "^2.1.1",
    "date-fns": "^3.6.0"
  },
  "devDependencies": {
    "@types/react": "^18.3.5",
    "@types/react-dom": "^18.3.0",
    "@vitejs/plugin-react": "^4.3.1",
    "autoprefixer": "^10.4.20",
    "postcss": "^8.4.45",
    "tailwindcss": "^3.4.11",
    "vite": "^5.4.2"
  }
}
```

### `vite.config.js`

```js
import { defineConfig } from 'vite'
import react from '@vitejs/plugin-react'

export default defineConfig({
  plugins: [react()],
  resolve: {
    alias: {
      '@': '/src',
    },
  },
})
```

### `tailwind.config.js`

```js
/** @type {import('tailwindcss').Config} */
export default {
  content: ['./index.html', './src/**/*.{js,ts,jsx,tsx}'],
  darkMode: 'class',
  theme: {
    extend: {
      colors: {
        crisis: {
          red:     '#FF1A1A',
          orange:  '#FF6B1A',
          yellow:  '#FFD700',
          cyan:    '#00F5FF',
          green:   '#00FF88',
          bg:      '#040810',
          surface: '#070D1A',
          card:    '#0A1428',
          border:  '#1A2E4A',
          muted:   '#2A3F5F',
          text:    '#B0C4DE',
        },
      },
      fontFamily: {
        mono:    ['"JetBrains Mono"', '"Fira Code"', 'monospace'],
        display: ['"Orbitron"', 'sans-serif'],
        body:    ['"Exo 2"', 'sans-serif'],
      },
      animation: {
        'pulse-red':   'pulseRed 1.5s ease-in-out infinite',
        'scan-line':   'scanLine 3s linear infinite',
        'flicker':     'flicker 0.15s infinite',
        'slide-in':    'slideIn 0.4s cubic-bezier(0.16,1,0.3,1)',
        'glow-pulse':  'glowPulse 2s ease-in-out infinite',
        'radar-spin':  'radarSpin 4s linear infinite',
        'blink':       'blink 1s step-end infinite',
      },
      keyframes: {
        pulseRed: {
          '0%,100%': { boxShadow: '0 0 0 0 rgba(255,26,26,0.7)' },
          '50%':     { boxShadow: '0 0 0 12px rgba(255,26,26,0)' },
        },
        scanLine: {
          '0%':   { transform: 'translateY(-100%)' },
          '100%': { transform: 'translateY(100vh)' },
        },
        flicker: {
          '0%,100%': { opacity: '1' },
          '50%':     { opacity: '0.85' },
        },
        slideIn: {
          from: { opacity: '0', transform: 'translateX(-20px)' },
          to:   { opacity: '1', transform: 'translateX(0)' },
        },
        glowPulse: {
          '0%,100%': { filter: 'drop-shadow(0 0 4px #00F5FF)' },
          '50%':     { filter: 'drop-shadow(0 0 12px #00F5FF)' },
        },
        radarSpin: {
          from: { transform: 'rotate(0deg)' },
          to:   { transform: 'rotate(360deg)' },
        },
        blink: {
          '0%,100%': { opacity: '1' },
          '50%':     { opacity: '0' },
        },
      },
      backgroundImage: {
        'grid-pattern': `linear-gradient(rgba(0,245,255,0.03) 1px, transparent 1px),
                         linear-gradient(90deg, rgba(0,245,255,0.03) 1px, transparent 1px)`,
        'crisis-gradient': 'linear-gradient(135deg, #040810 0%, #070D1A 50%, #040810 100%)',
      },
      backgroundSize: {
        'grid': '40px 40px',
      },
    },
  },
  plugins: [],
}
```

### `src/index.css`

```css
@import url('https://fonts.googleapis.com/css2?family=Orbitron:wght@400;600;700;900&family=Exo+2:wght@300;400;500;600&family=JetBrains+Mono:wght@400;500&display=swap');

@tailwind base;
@tailwind components;
@tailwind utilities;

:root {
  --crisis-red:    #FF1A1A;
  --crisis-cyan:   #00F5FF;
  --crisis-green:  #00FF88;
  --crisis-orange: #FF6B1A;
  --crisis-bg:     #040810;
}

* { box-sizing: border-box; margin: 0; padding: 0; }

body {
  background-color: var(--crisis-bg);
  color: #B0C4DE;
  font-family: 'Exo 2', sans-serif;
  overflow-x: hidden;
}

/* Scrollbar */
::-webkit-scrollbar       { width: 4px; }
::-webkit-scrollbar-track { background: #040810; }
::-webkit-scrollbar-thumb { background: #1A2E4A; border-radius: 2px; }

/* CRT scanline overlay */
.crt-overlay::before {
  content: '';
  position: fixed;
  inset: 0;
  background: repeating-linear-gradient(
    0deg,
    transparent,
    transparent 2px,
    rgba(0, 0, 0, 0.05) 2px,
    rgba(0, 0, 0, 0.05) 4px
  );
  pointer-events: none;
  z-index: 9999;
}

/* Neon glow text */
.glow-red    { text-shadow: 0 0 10px #FF1A1A, 0 0 20px #FF1A1A; }
.glow-cyan   { text-shadow: 0 0 10px #00F5FF, 0 0 20px #00F5FF; }
.glow-green  { text-shadow: 0 0 10px #00FF88; }

/* Border glow */
.border-glow-red  { box-shadow: 0 0 0 1px #FF1A1A, 0 0 20px rgba(255,26,26,0.3); }
.border-glow-cyan { box-shadow: 0 0 0 1px #00F5FF, 0 0 20px rgba(0,245,255,0.2); }

/* Hex grid background */
.hex-bg {
  background-color: #040810;
  background-image: url("data:image/svg+xml,%3Csvg xmlns='http://www.w3.org/2000/svg' width='28' height='49' viewBox='0 0 28 49'%3E%3Cg fill='%2300F5FF' fill-opacity='0.03'%3E%3Cpolygon points='14 0 28 7.5 28 22.5 14 30 0 22.5 0 7.5'/%3E%3C/g%3E%3C/svg%3E");
}

/* Incident card critical state */
.incident-critical {
  animation: criticalPulse 2s ease-in-out infinite;
  border-color: var(--crisis-red) !important;
}

@keyframes criticalPulse {
  0%,100% { box-shadow: 0 0 0 0 rgba(255,26,26,0.6), inset 0 0 30px rgba(255,26,26,0.05); }
  50%     { box-shadow: 0 0 0 6px rgba(255,26,26,0), inset 0 0 30px rgba(255,26,26,0.1); }
}

/* Map dot pulse */
.map-dot-critical {
  animation: mapPulse 1s ease-out infinite;
}

@keyframes mapPulse {
  0%   { transform: scale(1); opacity: 1; }
  100% { transform: scale(3); opacity: 0; }
}
```

---

## 2. Data Layer

### `src/data/incidents.js`

```js
export const INCIDENTS = [
  {
    id: 'INC-2024-001',
    type: 'Fire',
    location: 'Main Kitchen — Level B1',
    sensor_id: 'SN-402',
    timestamp: new Date(Date.now() - 2 * 60000).toISOString(),
    severity_level: 'Critical',
    status: 'Active',
    detected_by: 'Smoke Sensor + Camera AI',
    raw_value: '850ppm CO₂',
    ai_suggested_action: 'Evacuate floors B1–3. Deploy Fire Response Team Alpha. Notify BWSSB water unit. Alert guests via PA system. Close fire doors on Level 1.',
    affected_zones: ['B1-Kitchen', 'L1-Lobby', 'L2-Restaurant'],
    staff_assigned: ['Ravi Kumar (Security)', 'Priya Nair (Floor Manager)'],
    guest_count_affected: 47,
    evacuation_progress: 32,
    payload: { sensor_id: 'SN-402', type: 'smoke', location: 'Main Kitchen', raw_value: '850ppm' },
    coordinates: { x: 38, y: 72 },
  },
  {
    id: 'INC-2024-002',
    type: 'Medical Emergency',
    location: 'Pool Deck — Level 5',
    sensor_id: 'CAM-211',
    timestamp: new Date(Date.now() - 8 * 60000).toISOString(),
    severity_level: 'High',
    status: 'Acknowledged',
    detected_by: 'Camera AI (Fall Detection)',
    raw_value: 'Unconscious guest detected',
    ai_suggested_action: 'Dispatch trained first-aid staff immediately. Call 108 ambulance. Clear pool area. AED unit located at Concierge Desk L5.',
    affected_zones: ['L5-Pool', 'L5-Gym'],
    staff_assigned: ['Anjali Singh (Medical)', 'Suresh Patel (Security)'],
    guest_count_affected: 12,
    evacuation_progress: 0,
    payload: { sensor_id: 'CAM-211', type: 'fall_detection', location: 'Pool Deck L5', raw_value: 'unconscious_person' },
    coordinates: { x: 65, y: 28 },
  },
  {
    id: 'INC-2024-003',
    type: 'Security Threat',
    location: 'East Wing Entrance',
    sensor_id: 'ACC-105',
    timestamp: new Date(Date.now() - 15 * 60000).toISOString(),
    severity_level: 'Critical',
    status: 'Escalated',
    detected_by: 'Access Control + Facial Rec AI',
    raw_value: 'Unauthorized access attempt × 3',
    ai_suggested_action: 'Lock down East Wing. Alert all security staff. Activate CCTV recording on all East Wing cameras. Do NOT confront — await police.',
    affected_zones: ['EW-Entrance', 'EW-Corridor', 'EW-Room-201-215'],
    staff_assigned: ['Security Team Bravo', 'Mohan Das (Chief Security)'],
    guest_count_affected: 28,
    evacuation_progress: 0,
    payload: { sensor_id: 'ACC-105', type: 'access_breach', location: 'East Wing', raw_value: 'unauthorized_x3' },
    coordinates: { x: 82, y: 55 },
  },
  {
    id: 'INC-2024-004',
    type: 'Structural Alert',
    location: 'Rooftop Bar — Level 12',
    sensor_id: 'VIB-301',
    timestamp: new Date(Date.now() - 25 * 60000).toISOString(),
    severity_level: 'Medium',
    status: 'Monitoring',
    detected_by: 'Vibration Sensor Array',
    raw_value: '4.2g vibration anomaly',
    ai_suggested_action: 'Evacuate Rooftop Bar as precaution. Dispatch structural inspection team. Monitor sensors SN-301 through SN-308 continuously.',
    affected_zones: ['L12-Rooftop', 'L11-Events'],
    staff_assigned: ['Engineering Team'],
    guest_count_affected: 34,
    evacuation_progress: 78,
    payload: { sensor_id: 'VIB-301', type: 'vibration', location: 'Rooftop L12', raw_value: '4.2g' },
    coordinates: { x: 50, y: 15 },
  },
  {
    id: 'INC-2024-005',
    type: 'Flood / Water',
    location: 'Basement Parking — P2',
    sensor_id: 'WTR-089',
    timestamp: new Date(Date.now() - 40 * 60000).toISOString(),
    severity_level: 'High',
    status: 'Resolved',
    detected_by: 'Water Level Sensor',
    raw_value: 'Water level: 18cm',
    ai_suggested_action: 'Activate drainage pumps P2-A and P2-B. Close P2 entry gate. Reroute vehicles to P1. Alert maintenance immediately.',
    affected_zones: ['P2-Parking'],
    staff_assigned: ['Maintenance Team'],
    guest_count_affected: 0,
    evacuation_progress: 100,
    payload: { sensor_id: 'WTR-089', type: 'water_level', location: 'Basement P2', raw_value: '18cm' },
    coordinates: { x: 25, y: 88 },
  },
];

export const SEVERITY_CONFIG = {
  Critical: { color: 'text-crisis-red',    bg: 'bg-red-950',    border: 'border-crisis-red',    icon: '🔴', pulse: true },
  High:     { color: 'text-crisis-orange', bg: 'bg-orange-950', border: 'border-crisis-orange',  icon: '🟠', pulse: false },
  Medium:   { color: 'text-crisis-yellow', bg: 'bg-yellow-950', border: 'border-yellow-600',     icon: '🟡', pulse: false },
  Low:      { color: 'text-crisis-green',  bg: 'bg-green-950',  border: 'border-crisis-green',   icon: '🟢', pulse: false },
};
```

### `src/data/sensors.js`

```js
export const SENSORS = [
  { id: 'SN-101', name: 'Lobby Smoke Detector',    zone: 'L1-Lobby',    type: 'smoke',       status: 'Normal',  value: '12ppm',   lastPing: '2s ago' },
  { id: 'SN-402', name: 'Kitchen Smoke Detector',  zone: 'B1-Kitchen',  type: 'smoke',       status: 'Alert',   value: '850ppm',  lastPing: '1s ago' },
  { id: 'CAM-211', name: 'Pool Deck Camera',        zone: 'L5-Pool',     type: 'camera',      status: 'Alert',   value: 'Anomaly', lastPing: '3s ago' },
  { id: 'ACC-105', name: 'East Wing Access',        zone: 'EW-Entrance', type: 'access',      status: 'Breach',  value: 'LOCKED',  lastPing: '0s ago' },
  { id: 'VIB-301', name: 'Rooftop Vibration',       zone: 'L12-Roof',    type: 'vibration',   status: 'Warning', value: '4.2g',    lastPing: '5s ago' },
  { id: 'WTR-089', name: 'Basement Water Level',    zone: 'P2-Parking',  type: 'water',       status: 'Normal',  value: '2cm',     lastPing: '4s ago' },
  { id: 'TEMP-55', name: 'Server Room Temp',        zone: 'B2-IT Room',  type: 'temperature', status: 'Normal',  value: '22°C',    lastPing: '6s ago' },
  { id: 'GAS-30',  name: 'Kitchen Gas Sensor',      zone: 'B1-Kitchen',  type: 'gas',         status: 'Warning', value: '18%LEL',  lastPing: '2s ago' },
  { id: 'MOT-77',  name: 'Corridor Motion (East)',  zone: 'EW-Corridor', type: 'motion',      status: 'Active',  value: 'Moving',  lastPing: '1s ago' },
  { id: 'PWR-01',  name: 'Main Power Grid',         zone: 'B2-Utility',  type: 'power',       status: 'Normal',  value: '230V',    lastPing: '7s ago' },
];

export const SENSOR_TYPE_ICONS = {
  smoke:       '💨',
  camera:      '📷',
  access:      '🔒',
  vibration:   '📳',
  water:       '💧',
  temperature: '🌡️',
  gas:         '⚗️',
  motion:      '👁️',
  power:       '⚡',
};
```

### `src/data/staff.js`

```js
export const STAFF = [
  { id: 'ST-01', name: 'Ravi Kumar',    role: 'Security Chief',  status: 'On Duty',    zone: 'B1-Kitchen',    avatar: 'RK', responding: true },
  { id: 'ST-02', name: 'Priya Nair',    role: 'Floor Manager',   status: 'On Duty',    zone: 'L1-Lobby',      avatar: 'PN', responding: true },
  { id: 'ST-03', name: 'Anjali Singh',  role: 'Medical Officer', status: 'Responding', zone: 'L5-Pool',       avatar: 'AS', responding: true },
  { id: 'ST-04', name: 'Suresh Patel',  role: 'Security Guard',  status: 'On Duty',    zone: 'EW-Entrance',   avatar: 'SP', responding: true },
  { id: 'ST-05', name: 'Meera Joshi',   role: 'Front Desk',      status: 'On Duty',    zone: 'L1-Reception',  avatar: 'MJ', responding: false },
  { id: 'ST-06', name: 'Mohan Das',     role: 'Duty Manager',    status: 'On Duty',    zone: 'Control Room',  avatar: 'MD', responding: false },
  { id: 'ST-07', name: 'Kavya Reddy',   role: 'Housekeeping',    status: 'Break',      zone: 'L7-Staff Room', avatar: 'KR', responding: false },
  { id: 'ST-08', name: 'Arjun Sharma',  role: 'Maintenance',     status: 'On Duty',    zone: 'P2-Parking',    avatar: 'AR', responding: false },
];
```

### `src/data/mapData.js`

```js
export const PROPERTY_ZONES = [
  { id: 'L1-Lobby',      label: 'Lobby',         x: 30, y: 75, w: 40, h: 15, floor: 1,   color: 'rgba(0,245,255,0.08)' },
  { id: 'L1-Reception',  label: 'Reception',      x: 72, y: 75, w: 20, h: 15, floor: 1,   color: 'rgba(0,245,255,0.05)' },
  { id: 'B1-Kitchen',    label: 'Kitchen',        x: 10, y: 75, w: 18, h: 15, floor: -1,  color: 'rgba(255,26,26,0.2)' },
  { id: 'EW-Entrance',   label: 'East Entrance',  x: 75, y: 50, w: 22, h: 18, floor: 1,   color: 'rgba(255,26,26,0.15)' },
  { id: 'L5-Pool',       label: 'Pool Deck',      x: 55, y: 20, w: 35, h: 18, floor: 5,   color: 'rgba(255,107,26,0.15)' },
  { id: 'L12-Rooftop',   label: 'Rooftop Bar',    x: 30, y: 5,  w: 40, h: 10, floor: 12,  color: 'rgba(255,215,0,0.1)' },
  { id: 'P2-Parking',    label: 'Parking P2',     x: 10, y: 88, w: 80, h: 10, floor: -2,  color: 'rgba(0,255,136,0.05)' },
  { id: 'L2-Restaurant', label: 'Restaurant',     x: 10, y: 57, w: 40, h: 15, floor: 2,   color: 'rgba(0,245,255,0.05)' },
  { id: 'B2-IT Room',    label: 'IT / Server',    x: 55, y: 88, w: 20, h: 10, floor: -2,  color: 'rgba(0,245,255,0.08)' },
];

export const EVAC_ROUTES = [
  { from: { x: 19, y: 74 }, to: { x: 19, y: 98 }, label: 'Route A', active: true },
  { from: { x: 50, y: 74 }, to: { x: 50, y: 98 }, label: 'Route B', active: true },
  { from: { x: 78, y: 60 }, to: { x: 95, y: 60 }, label: 'Route C (blocked)', active: false },
];
```

---

## 3. Context

### `src/context/CrisisContext.jsx`

```jsx
import { createContext, useContext, useState, useEffect, useCallback } from 'react';
import { INCIDENTS } from '../data/incidents';
import { SENSORS } from '../data/sensors';
import { STAFF } from '../data/staff';

const CrisisContext = createContext(null);

export function CrisisProvider({ children }) {
  const [incidents, setIncidents]       = useState(INCIDENTS);
  const [sensors, setSensors]           = useState(SENSORS);
  const [staff]                         = useState(STAFF);
  const [activeIncident, setActiveIncident] = useState(null);
  const [showBroadcast, setShowBroadcast]   = useState(false);
  const [showEscalate, setShowEscalate]     = useState(false);
  const [broadcastTarget, setBroadcastTarget] = useState(null);
  const [alarmActive, setAlarmActive]   = useState(false);
  const [notifications, setNotifications] = useState([]);

  // Simulate live sensor fluctuations
  useEffect(() => {
    const interval = setInterval(() => {
      setSensors(prev => prev.map(s => {
        if (s.status === 'Alert' || s.status === 'Breach') return s;
        const rand = Math.random();
        return { ...s, lastPing: `${Math.floor(rand * 10)}s ago` };
      }));
    }, 3000);
    return () => clearInterval(interval);
  }, []);

  // Simulate incoming incident
  useEffect(() => {
    const timer = setTimeout(() => {
      const newIncident = {
        id: 'INC-2024-006',
        type: 'Power Outage',
        location: 'North Wing — Levels 8–10',
        sensor_id: 'PWR-08',
        timestamp: new Date().toISOString(),
        severity_level: 'High',
        status: 'New',
        detected_by: 'Power Grid Monitor',
        raw_value: 'Voltage drop: 0V',
        ai_suggested_action: 'Switch to backup generator. Notify guests on L8–L10. Deploy staff for elevator assistance. Estimated restore: 12 min.',
        affected_zones: ['L8', 'L9', 'L10'],
        staff_assigned: [],
        guest_count_affected: 62,
        evacuation_progress: 0,
        payload: { sensor_id: 'PWR-08', type: 'power', location: 'North Wing L8-10', raw_value: '0V' },
        coordinates: { x: 72, y: 42 },
      };
      setIncidents(prev => [newIncident, ...prev]);
      pushNotification('⚡ New Incident: Power Outage — North Wing L8–L10', 'warning');
    }, 12000);
    return () => clearTimeout(timer);
  }, []);

  const pushNotification = useCallback((message, type = 'info') => {
    const id = Date.now();
    setNotifications(prev => [{ id, message, type, time: new Date() }, ...prev.slice(0, 9)]);
    setTimeout(() => {
      setNotifications(prev => prev.filter(n => n.id !== id));
    }, 6000);
  }, []);

  const acknowledgeIncident = useCallback((incidentId) => {
    setIncidents(prev => prev.map(i =>
      i.id === incidentId ? { ...i, status: 'Acknowledged' } : i
    ));
    pushNotification(`✓ Incident ${incidentId} acknowledged`, 'success');
  }, [pushNotification]);

  const resolveIncident = useCallback((incidentId) => {
    setIncidents(prev => prev.map(i =>
      i.id === incidentId ? { ...i, status: 'Resolved', evacuation_progress: 100 } : i
    ));
    pushNotification(`✅ Incident ${incidentId} resolved`, 'success');
  }, [pushNotification]);

  const triggerSOS = useCallback(() => {
    setAlarmActive(true);
    pushNotification('🚨 SOS TRIGGERED — All stations alerted', 'critical');
    setTimeout(() => setAlarmActive(false), 10000);
  }, [pushNotification]);

  const criticalCount = incidents.filter(i => i.severity_level === 'Critical' && i.status !== 'Resolved').length;
  const activeCount   = incidents.filter(i => i.status === 'Active' || i.status === 'New').length;

  return (
    <CrisisContext.Provider value={{
      incidents, sensors, staff,
      activeIncident, setActiveIncident,
      showBroadcast, setShowBroadcast,
      showEscalate,  setShowEscalate,
      broadcastTarget, setBroadcastTarget,
      alarmActive, triggerSOS,
      notifications,
      criticalCount, activeCount,
      acknowledgeIncident, resolveIncident,
      pushNotification,
    }}>
      {children}
    </CrisisContext.Provider>
  );
}

export const useCrisis = () => {
  const ctx = useContext(CrisisContext);
  if (!ctx) throw new Error('useCrisis must be used within CrisisProvider');
  return ctx;
};
```

---

## 4. UI Primitives

### `src/components/ui/PulsingDot.jsx`

```jsx
export function PulsingDot({ color = 'bg-crisis-red', size = 'w-2.5 h-2.5' }) {
  return (
    <span className="relative flex shrink-0">
      <span className={`animate-ping absolute inline-flex h-full w-full rounded-full ${color} opacity-75`} />
      <span className={`relative inline-flex rounded-full ${size} ${color}`} />
    </span>
  );
}
```

### `src/components/ui/StatusBadge.jsx`

```jsx
const STATUS_STYLES = {
  Active:       'bg-red-900/80 text-crisis-red border border-crisis-red/50',
  Critical:     'bg-red-900/80 text-crisis-red border border-crisis-red animate-pulse',
  New:          'bg-orange-900/80 text-crisis-orange border border-crisis-orange/50',
  Acknowledged: 'bg-blue-900/80 text-blue-300 border border-blue-500/50',
  Monitoring:   'bg-yellow-900/80 text-crisis-yellow border border-yellow-500/50',
  Escalated:    'bg-purple-900/80 text-purple-300 border border-purple-500/50',
  Resolved:     'bg-green-900/80 text-crisis-green border border-crisis-green/50',
  Normal:       'bg-green-900/50 text-crisis-green border border-crisis-green/30',
  Warning:      'bg-yellow-900/50 text-crisis-yellow border border-yellow-500/30',
  Alert:        'bg-red-900/50 text-crisis-red border border-crisis-red/50 animate-pulse',
  Breach:       'bg-red-900/80 text-crisis-red border border-crisis-red animate-pulse',
};

export function StatusBadge({ status }) {
  return (
    <span className={`px-2 py-0.5 rounded text-[10px] font-mono font-semibold tracking-widest uppercase ${STATUS_STYLES[status] || STATUS_STYLES.Normal}`}>
      {status}
    </span>
  );
}
```

### `src/components/ui/SOSButton.jsx`

```jsx
import { useCrisis } from '../../context/CrisisContext';
import { AlertTriangle } from 'lucide-react';
import { useState } from 'react';

export function SOSButton() {
  const { triggerSOS, alarmActive } = useCrisis();
  const [held, setHeld] = useState(false);
  const [holdTimer, setHoldTimer] = useState(null);
  const [holdProgress, setHoldProgress] = useState(0);

  const handleMouseDown = () => {
    setHeld(true);
    let progress = 0;
    const interval = setInterval(() => {
      progress += 5;
      setHoldProgress(progress);
      if (progress >= 100) {
        clearInterval(interval);
        triggerSOS();
        setHeld(false);
        setHoldProgress(0);
      }
    }, 100);
    setHoldTimer(interval);
  };

  const handleMouseUp = () => {
    clearInterval(holdTimer);
    setHeld(false);
    setHoldProgress(0);
  };

  return (
    <div className="flex flex-col items-center gap-2">
      <div className="relative">
        {/* Outer ring */}
        <svg className="absolute inset-0 w-full h-full -rotate-90" viewBox="0 0 64 64">
          <circle cx="32" cy="32" r="28" fill="none" stroke="#1A2E4A" strokeWidth="3" />
          {held && (
            <circle
              cx="32" cy="32" r="28"
              fill="none"
              stroke="#FF1A1A"
              strokeWidth="3"
              strokeDasharray={`${holdProgress * 1.76} 176`}
              strokeLinecap="round"
            />
          )}
        </svg>
        <button
          onMouseDown={handleMouseDown}
          onMouseUp={handleMouseUp}
          onMouseLeave={handleMouseUp}
          onTouchStart={handleMouseDown}
          onTouchEnd={handleMouseUp}
          className={`
            relative w-16 h-16 rounded-full border-2
            flex flex-col items-center justify-center gap-0.5
            font-display font-black text-[9px] tracking-widest
            transition-all duration-150 select-none
            ${alarmActive
              ? 'bg-crisis-red border-crisis-red text-white animate-pulse-red shadow-[0_0_30px_rgba(255,26,26,0.8)]'
              : 'bg-red-950 border-crisis-red/70 text-crisis-red hover:bg-red-900 hover:shadow-[0_0_20px_rgba(255,26,26,0.5)]'
            }
          `}
        >
          <AlertTriangle size={20} />
          <span>SOS</span>
        </button>
      </div>
      <p className="text-crisis-muted text-[9px] font-mono text-center leading-tight">
        {held ? 'HOLD…' : 'HOLD 2s'}
      </p>
    </div>
  );
}
```

### `src/components/ui/AnimatedCounter.jsx`

```jsx
import { useEffect, useState } from 'react';

export function AnimatedCounter({ value, className }) {
  const [display, setDisplay] = useState(0);

  useEffect(() => {
    const step = value > display ? 1 : -1;
    if (display === value) return;
    const t = setTimeout(() => setDisplay(d => d + step), 30);
    return () => clearTimeout(t);
  }, [value, display]);

  return <span className={className}>{display}</span>;
}
```

---

## 5. Layout Components

### `src/components/layout/Header.jsx`

```jsx
import { Bell, Radio, Wifi, Shield, Clock } from 'lucide-react';
import { useCrisis } from '../../context/CrisisContext';
import { SOSButton } from '../ui/SOSButton';
import { AnimatedCounter } from '../ui/AnimatedCounter';
import { useEffect, useState } from 'react';
import { Link, useLocation } from 'react-router-dom';

const NAV_LINKS = [
  { to: '/dashboard',    label: 'CONTROL ROOM' },
  { to: '/incidents',    label: 'INCIDENT LOG' },
  { to: '/digital-twin', label: 'DIGITAL TWIN' },
  { to: '/voice',        label: 'VOICE AI' },
  { to: '/reports',      label: 'REPORTS' },
];

export function Header({ user }) {
  const { criticalCount, activeCount, alarmActive, notifications } = useCrisis();
  const location = useLocation();
  const [time, setTime] = useState(new Date());

  useEffect(() => {
    const t = setInterval(() => setTime(new Date()), 1000);
    return () => clearInterval(t);
  }, []);

  return (
    <header className={`
      h-16 flex items-center justify-between px-4 border-b border-crisis-border
      bg-crisis-surface z-50 relative shrink-0
      ${alarmActive ? 'animate-flicker' : ''}
    `}>
      {/* Left: Logo + Nav */}
      <div className="flex items-center gap-6">
        <div className="flex items-center gap-2.5">
          <div className="relative">
            <Shield size={28} className="text-crisis-cyan animate-glow-pulse" />
            {criticalCount > 0 && (
              <span className="absolute -top-1 -right-1 w-4 h-4 rounded-full bg-crisis-red text-white text-[9px] flex items-center justify-center font-bold animate-pulse">
                {criticalCount}
              </span>
            )}
          </div>
          <div>
            <p className="font-display font-bold text-crisis-cyan text-sm tracking-widest leading-none glow-cyan">
              CRISISSYNC
            </p>
            <p className="text-crisis-muted text-[9px] font-mono tracking-widest">AI RESPONSE SYSTEM</p>
          </div>
        </div>

        <nav className="hidden lg:flex items-center gap-1">
          {NAV_LINKS.map(({ to, label }) => (
            <Link
              key={to}
              to={to}
              className={`
                px-3 py-1.5 rounded text-[10px] font-mono tracking-widest font-medium
                transition-all duration-200
                ${location.pathname === to
                  ? 'bg-crisis-cyan/10 text-crisis-cyan border border-crisis-cyan/30'
                  : 'text-crisis-text hover:text-crisis-cyan hover:bg-crisis-cyan/5'
                }
              `}
            >
              {label}
            </Link>
          ))}
        </nav>
      </div>

      {/* Center: Live Status */}
      <div className="hidden md:flex items-center gap-6 absolute left-1/2 -translate-x-1/2">
        <div className="flex items-center gap-2 bg-red-950/50 border border-crisis-red/30 rounded px-3 py-1.5">
          <span className="w-2 h-2 rounded-full bg-crisis-red animate-pulse" />
          <span className="text-crisis-red font-mono text-xs font-semibold">
            <AnimatedCounter value={criticalCount} /> CRITICAL
          </span>
        </div>
        <div className="flex items-center gap-2 bg-crisis-card border border-crisis-border rounded px-3 py-1.5">
          <Radio size={12} className="text-crisis-orange animate-pulse" />
          <span className="text-crisis-orange font-mono text-xs">
            <AnimatedCounter value={activeCount} /> ACTIVE
          </span>
        </div>
        <div className="flex items-center gap-2 bg-crisis-card border border-crisis-border rounded px-3 py-1.5">
          <Wifi size={12} className="text-crisis-green" />
          <span className="text-crisis-green font-mono text-xs">LIVE</span>
        </div>
      </div>

      {/* Right: Clock + SOS + User */}
      <div className="flex items-center gap-4">
        <div className="hidden sm:flex flex-col items-end">
          <span className="font-mono text-crisis-cyan text-sm glow-cyan">
            {time.toLocaleTimeString('en-IN', { hour12: false })}
          </span>
          <span className="font-mono text-crisis-muted text-[10px]">
            {time.toLocaleDateString('en-IN', { day: '2-digit', month: 'short', year: 'numeric' })}
          </span>
        </div>

        <SOSButton />

        <div className="flex items-center gap-2 bg-crisis-card border border-crisis-border rounded-lg px-3 py-2">
          <div className="w-7 h-7 rounded-full bg-crisis-cyan/20 border border-crisis-cyan/40 flex items-center justify-center text-crisis-cyan font-bold text-xs">
            {user?.avatar || 'MG'}
          </div>
          <div className="hidden sm:block">
            <p className="text-crisis-text text-xs font-medium leading-none">{user?.name || 'Manager'}</p>
            <p className="text-crisis-muted text-[9px] font-mono">{user?.role || 'HOTEL MGR'}</p>
          </div>
        </div>
      </div>
    </header>
  );
}
```

### `src/components/layout/Sidebar.jsx`

```jsx
import { useCrisis } from '../../context/CrisisContext';
import { StatusBadge } from '../ui/StatusBadge';
import { PulsingDot } from '../ui/PulsingDot';
import { SENSOR_TYPE_ICONS } from '../../data/sensors';
import { Users, Cpu, BellRing, ChevronDown, ChevronUp } from 'lucide-react';
import { useState } from 'react';

function SensorRow({ sensor }) {
  const isAlert = sensor.status === 'Alert' || sensor.status === 'Breach';
  return (
    <div className={`
      flex items-center justify-between py-2 px-3 rounded
      border transition-all duration-300
      ${isAlert ? 'bg-red-950/30 border-crisis-red/30' : 'bg-crisis-card/50 border-crisis-border/50'}
    `}>
      <div className="flex items-center gap-2 min-w-0">
        <span className="text-sm shrink-0">{SENSOR_TYPE_ICONS[sensor.type] || '📡'}</span>
        <div className="min-w-0">
          <p className={`text-[11px] font-medium truncate ${isAlert ? 'text-crisis-red' : 'text-crisis-text'}`}>
            {sensor.name}
          </p>
          <p className="text-crisis-muted text-[9px] font-mono truncate">{sensor.zone}</p>
        </div>
      </div>
      <div className="flex flex-col items-end gap-0.5 shrink-0 ml-2">
        <StatusBadge status={sensor.status} />
        <span className="text-crisis-muted text-[9px] font-mono">{sensor.lastPing}</span>
      </div>
    </div>
  );
}

function StaffRow({ member }) {
  const isResponding = member.responding;
  return (
    <div className="flex items-center gap-2 py-1.5 px-2 rounded bg-crisis-card/50 border border-crisis-border/50">
      <div className={`
        w-7 h-7 rounded-full flex items-center justify-center text-xs font-bold shrink-0
        ${isResponding ? 'bg-crisis-red/20 border border-crisis-red/50 text-crisis-red' : 'bg-crisis-cyan/10 border border-crisis-cyan/30 text-crisis-cyan'}
      `}>
        {member.avatar}
      </div>
      <div className="min-w-0 flex-1">
        <p className="text-crisis-text text-[11px] font-medium truncate">{member.name}</p>
        <p className="text-crisis-muted text-[9px] font-mono truncate">{member.zone}</p>
      </div>
      <div className="flex items-center gap-1 shrink-0">
        {isResponding && <PulsingDot color="bg-crisis-red" size="w-1.5 h-1.5" />}
        <span className={`text-[9px] font-mono ${isResponding ? 'text-crisis-red' : 'text-crisis-green'}`}>
          {isResponding ? 'RESP' : 'ON'}
        </span>
      </div>
    </div>
  );
}

export function Sidebar() {
  const { sensors, staff } = useCrisis();
  const [sensorOpen, setSensorOpen] = useState(true);
  const [staffOpen, setStaffOpen]   = useState(true);

  const alertSensors  = sensors.filter(s => s.status !== 'Normal' && s.status !== 'Active');
  const normalSensors = sensors.filter(s => s.status === 'Normal' || s.status === 'Active');

  return (
    <aside className="w-64 shrink-0 bg-crisis-surface border-r border-crisis-border flex flex-col overflow-y-auto">
      {/* Sensors Panel */}
      <div className="border-b border-crisis-border">
        <button
          onClick={() => setSensorOpen(o => !o)}
          className="w-full flex items-center justify-between px-4 py-3 hover:bg-crisis-card/50 transition-colors"
        >
          <div className="flex items-center gap-2">
            <Cpu size={14} className="text-crisis-cyan" />
            <span className="font-display text-[11px] tracking-widest text-crisis-text font-semibold">SENSORS</span>
            <span className="bg-crisis-red text-white text-[9px] rounded px-1.5 py-0.5 font-mono font-bold">
              {alertSensors.length} ALERT
            </span>
          </div>
          {sensorOpen ? <ChevronUp size={12} className="text-crisis-muted" /> : <ChevronDown size={12} className="text-crisis-muted" />}
        </button>

        {sensorOpen && (
          <div className="px-2 pb-3 space-y-1.5">
            {alertSensors.length > 0 && (
              <>
                <p className="text-crisis-red text-[9px] font-mono px-1 py-1 tracking-widest">⚠ ALERTS</p>
                {alertSensors.map(s => <SensorRow key={s.id} sensor={s} />)}
                <p className="text-crisis-muted text-[9px] font-mono px-1 py-1 tracking-widest">NORMAL</p>
              </>
            )}
            {normalSensors.map(s => <SensorRow key={s.id} sensor={s} />)}
          </div>
        )}
      </div>

      {/* Staff Panel */}
      <div>
        <button
          onClick={() => setStaffOpen(o => !o)}
          className="w-full flex items-center justify-between px-4 py-3 hover:bg-crisis-card/50 transition-colors"
        >
          <div className="flex items-center gap-2">
            <Users size={14} className="text-crisis-cyan" />
            <span className="font-display text-[11px] tracking-widest text-crisis-text font-semibold">STAFF</span>
            <span className="bg-crisis-orange text-white text-[9px] rounded px-1.5 py-0.5 font-mono font-bold">
              {staff.filter(s => s.responding).length} RESP
            </span>
          </div>
          {staffOpen ? <ChevronUp size={12} className="text-crisis-muted" /> : <ChevronDown size={12} className="text-crisis-muted" />}
        </button>

        {staffOpen && (
          <div className="px-2 pb-3 space-y-1.5">
            {staff.map(m => <StaffRow key={m.id} member={m} />)}
          </div>
        )}
      </div>

      {/* Notifications */}
      <div className="mt-auto border-t border-crisis-border p-3">
        <div className="flex items-center gap-2 mb-2">
          <BellRing size={12} className="text-crisis-cyan" />
          <span className="text-[10px] font-mono text-crisis-muted tracking-widest">SYSTEM LOG</span>
        </div>
        <div className="space-y-1">
          <p className="text-[10px] font-mono text-crisis-green">✓ Backup generator online</p>
          <p className="text-[10px] font-mono text-crisis-yellow">⚠ Elevator B stuck at L5</p>
          <p className="text-[10px] font-mono text-crisis-muted">→ Fire dept. ETA: 4 min</p>
          <p className="text-[10px] font-mono text-crisis-muted">→ 108 ETA: 7 min</p>
        </div>
      </div>
    </aside>
  );
}
```

### `src/components/layout/RightPanel.jsx`

```jsx
import { PropertyMap }        from '../dashboard/PropertyMap';
import { EvacuationProgress } from '../dashboard/EvacuationProgress';
import { AlertsBroadcast }    from '../dashboard/AlertsBroadcast';

export function RightPanel() {
  return (
    <aside className="w-80 shrink-0 bg-crisis-surface border-l border-crisis-border flex flex-col overflow-y-auto">
      <PropertyMap />
      <EvacuationProgress />
      <AlertsBroadcast />
    </aside>
  );
}
```

---

## 6. Dashboard Components

### `src/components/dashboard/IncidentCard.jsx`

```jsx
import { motion, AnimatePresence } from 'framer-motion';
import { useCrisis } from '../../context/CrisisContext';
import { StatusBadge } from '../ui/StatusBadge';
import { SEVERITY_CONFIG } from '../../data/incidents';
import {
  AlertTriangle, Brain, Radio, PhoneCall,
  CheckCircle, ChevronDown, ChevronUp,
  MapPin, Users, Clock
} from 'lucide-react';
import { useState } from 'react';
import { formatDistanceToNow } from 'date-fns';

const INCIDENT_ICONS = {
  Fire:             '🔥',
  'Medical Emergency': '🏥',
  'Security Threat': '🛡️',
  'Structural Alert': '🏗️',
  'Flood / Water':   '💧',
  'Power Outage':    '⚡',
};

export function IncidentCard({ incident }) {
  const { acknowledgeIncident, resolveIncident, setShowBroadcast, setBroadcastTarget, setShowEscalate, setActiveIncident } = useCrisis();
  const [expanded, setExpanded] = useState(false);
  const cfg = SEVERITY_CONFIG[incident.severity_level] || SEVERITY_CONFIG.Low;
  const isCritical = incident.severity_level === 'Critical';
  const isResolved = incident.status === 'Resolved';

  return (
    <motion.div
      layout
      initial={{ opacity: 0, x: -30 }}
      animate={{ opacity: 1, x: 0 }}
      exit={{ opacity: 0, x: 30 }}
      transition={{ duration: 0.4, ease: [0.16, 1, 0.3, 1] }}
      className={`
        rounded-lg border bg-crisis-card overflow-hidden
        ${cfg.border}
        ${isCritical && !isResolved ? 'incident-critical' : ''}
        ${isResolved ? 'opacity-50' : ''}
      `}
    >
      {/* Critical Banner */}
      {isCritical && !isResolved && (
        <div className="bg-crisis-red/20 border-b border-crisis-red/50 px-4 py-1.5 flex items-center gap-2">
          <AlertTriangle size={12} className="text-crisis-red animate-pulse shrink-0" />
          <span className="text-crisis-red font-mono text-[10px] font-bold tracking-[0.2em] animate-pulse">
            ██ CRITICAL INCIDENT — IMMEDIATE ACTION REQUIRED ██
          </span>
        </div>
      )}

      {/* Header */}
      <div className="p-4">
        <div className="flex items-start justify-between gap-3">
          <div className="flex items-start gap-3 min-w-0">
            <span className="text-2xl shrink-0 mt-0.5">{INCIDENT_ICONS[incident.type] || '⚠️'}</span>
            <div className="min-w-0">
              <div className="flex items-center gap-2 flex-wrap mb-1">
                <h3 className={`font-display font-bold text-sm ${cfg.color}`}>{incident.type.toUpperCase()}</h3>
                <StatusBadge status={incident.status} />
                <StatusBadge status={incident.severity_level} />
              </div>
              <div className="flex items-center gap-1.5 text-crisis-muted text-xs">
                <MapPin size={10} className="shrink-0" />
                <span className="truncate">{incident.location}</span>
              </div>
              <div className="flex items-center gap-3 mt-1 text-[11px] font-mono text-crisis-muted">
                <span className="flex items-center gap-1">
                  <Clock size={9} />
                  {formatDistanceToNow(new Date(incident.timestamp), { addSuffix: true })}
                </span>
                <span>ID: {incident.id}</span>
              </div>
            </div>
          </div>

          <div className="flex items-center gap-2 shrink-0">
            <div className={`text-center px-2 py-1 rounded border ${cfg.border} ${cfg.bg}`}>
              <p className={`text-lg font-display font-black ${cfg.color}`}>{incident.guest_count_affected}</p>
              <p className="text-crisis-muted text-[8px] font-mono">GUESTS</p>
            </div>
            <button
              onClick={() => setExpanded(e => !e)}
              className="text-crisis-muted hover:text-crisis-cyan transition-colors p-1"
            >
              {expanded ? <ChevronUp size={16} /> : <ChevronDown size={16} />}
            </button>
          </div>
        </div>

        {/* AI Suggested Action */}
        {!isResolved && (
          <div className="mt-3 p-3 rounded bg-crisis-surface border border-crisis-cyan/20">
            <div className="flex items-start gap-2">
              <Brain size={12} className="text-crisis-cyan shrink-0 mt-0.5 animate-glow-pulse" />
              <div>
                <p className="text-crisis-cyan text-[9px] font-mono tracking-widest mb-1">AI SUGGESTED ACTION</p>
                <p className="text-crisis-text text-xs leading-relaxed">{incident.ai_suggested_action}</p>
              </div>
            </div>
          </div>
        )}

        {/* Action Buttons */}
        {!isResolved && (
          <div className="mt-3 flex flex-wrap gap-2">
            {incident.status !== 'Acknowledged' && incident.status !== 'Escalated' && (
              <button
                onClick={() => acknowledgeIncident(incident.id)}
                className="flex items-center gap-1.5 px-3 py-1.5 rounded text-xs font-semibold bg-blue-900/50 text-blue-300 border border-blue-500/40 hover:bg-blue-900/80 hover:border-blue-400 transition-all"
              >
                <CheckCircle size={12} />
                Acknowledge
              </button>
            )}

            <button
              onClick={() => {
                setBroadcastTarget(incident);
                setShowBroadcast(true);
              }}
              className={`
                flex items-center gap-1.5 px-3 py-1.5 rounded text-xs font-bold
                transition-all duration-200
                ${isCritical
                  ? 'bg-crisis-red text-white border border-crisis-red hover:bg-red-600 shadow-[0_0_15px_rgba(255,26,26,0.4)] animate-pulse-red'
                  : 'bg-crisis-orange/20 text-crisis-orange border border-crisis-orange/50 hover:bg-crisis-orange/30'
                }
              `}
            >
              <Radio size={12} />
              {isCritical ? '🔊 Broadcast Evacuation' : 'Broadcast Alert'}
            </button>

            <button
              onClick={() => {
                setActiveIncident(incident);
                setShowEscalate(true);
              }}
              className="flex items-center gap-1.5 px-3 py-1.5 rounded text-xs font-semibold bg-purple-900/30 text-purple-300 border border-purple-500/40 hover:bg-purple-900/60 transition-all"
            >
              <PhoneCall size={12} />
              Escalate to 911
            </button>

            <button
              onClick={() => resolveIncident(incident.id)}
              className="flex items-center gap-1.5 px-3 py-1.5 rounded text-xs font-semibold bg-green-900/30 text-crisis-green border border-crisis-green/40 hover:bg-green-900/60 transition-all ml-auto"
            >
              ✓ Mark Resolved
            </button>
          </div>
        )}
      </div>

      {/* Expanded Details */}
      <AnimatePresence>
        {expanded && (
          <motion.div
            initial={{ height: 0, opacity: 0 }}
            animate={{ height: 'auto', opacity: 1 }}
            exit={{ height: 0, opacity: 0 }}
            transition={{ duration: 0.3 }}
            className="overflow-hidden"
          >
            <div className="px-4 pb-4 border-t border-crisis-border pt-3 grid grid-cols-2 gap-3">
              <div>
                <p className="text-crisis-muted text-[9px] font-mono tracking-widest mb-1">DETECTED BY</p>
                <p className="text-crisis-text text-xs">{incident.detected_by}</p>
              </div>
              <div>
                <p className="text-crisis-muted text-[9px] font-mono tracking-widest mb-1">RAW VALUE</p>
                <p className="text-crisis-cyan text-xs font-mono">{incident.raw_value}</p>
              </div>
              <div>
                <p className="text-crisis-muted text-[9px] font-mono tracking-widest mb-1">SENSOR ID</p>
                <p className="text-crisis-text text-xs font-mono">{incident.sensor_id}</p>
              </div>
              <div>
                <p className="text-crisis-muted text-[9px] font-mono tracking-widest mb-1">AFFECTED ZONES</p>
                <div className="flex flex-wrap gap-1">
                  {incident.affected_zones.map(z => (
                    <span key={z} className="text-[9px] font-mono bg-crisis-muted/20 text-crisis-text px-1.5 py-0.5 rounded">{z}</span>
                  ))}
                </div>
              </div>
              {incident.staff_assigned.length > 0 && (
                <div className="col-span-2">
                  <p className="text-crisis-muted text-[9px] font-mono tracking-widest mb-1 flex items-center gap-1">
                    <Users size={9} /> STAFF ASSIGNED
                  </p>
                  <div className="flex flex-wrap gap-1">
                    {incident.staff_assigned.map(s => (
                      <span key={s} className="text-[10px] bg-crisis-cyan/10 text-crisis-cyan border border-crisis-cyan/20 px-2 py-0.5 rounded-full">{s}</span>
                    ))}
                  </div>
                </div>
              )}
              <div className="col-span-2">
                <p className="text-crisis-muted text-[9px] font-mono tracking-widest mb-1">API PAYLOAD</p>
                <pre className="text-crisis-green text-[10px] font-mono bg-black/40 p-2 rounded border border-crisis-border overflow-x-auto">
                  {JSON.stringify(incident.payload, null, 2)}
                </pre>
              </div>
            </div>
          </motion.div>
        )}
      </AnimatePresence>
    </motion.div>
  );
}
```

### `src/components/dashboard/PropertyMap.jsx`

```jsx
import { useCrisis } from '../../context/CrisisContext';
import { PROPERTY_ZONES, EVAC_ROUTES } from '../../data/mapData';
import { Map, Navigation } from 'lucide-react';

export function PropertyMap() {
  const { incidents } = useCrisis();
  const activeIncidents = incidents.filter(i => i.status !== 'Resolved');

  return (
    <div className="p-3 border-b border-crisis-border">
      <div className="flex items-center gap-2 mb-3">
        <Map size={13} className="text-crisis-cyan" />
        <span className="font-display text-[11px] tracking-widest text-crisis-text font-semibold">PROPERTY MAP</span>
        <span className="text-crisis-muted text-[9px] font-mono ml-auto">GRAND HYATT BENGALURU</span>
      </div>

      <div className="relative bg-crisis-bg border border-crisis-border rounded overflow-hidden" style={{ height: 200, backgroundImage: 'linear-gradient(rgba(0,245,255,0.02) 1px, transparent 1px), linear-gradient(90deg, rgba(0,245,255,0.02) 1px, transparent 1px)', backgroundSize: '10% 10%' }}>

        {/* Floors Label */}
        <div className="absolute left-1 top-1 flex flex-col gap-0.5">
          {['L12','L5','L2','L1','B1','P2'].map(f => (
            <span key={f} className="text-crisis-muted text-[8px] font-mono">{f}</span>
          ))}
        </div>

        {/* Zones */}
        {PROPERTY_ZONES.map(zone => (
          <div
            key={zone.id}
            className="absolute rounded border border-crisis-border/50 flex items-center justify-center"
            style={{ left: `${zone.x}%`, top: `${zone.y}%`, width: `${zone.w}%`, height: `${zone.h}%`, background: zone.color }}
          >
            <span className="text-[7px] font-mono text-crisis-muted text-center leading-tight px-0.5">{zone.label}</span>
          </div>
        ))}

        {/* Evacuation Routes */}
        <svg className="absolute inset-0 w-full h-full pointer-events-none">
          {EVAC_ROUTES.map((route, i) => (
            <line
              key={i}
              x1={`${route.from.x}%`} y1={`${route.from.y}%`}
              x2={`${route.to.x}%`}   y2={`${route.to.y}%`}
              stroke={route.active ? '#00FF88' : '#FF1A1A'}
              strokeWidth="1.5"
              strokeDasharray={route.active ? 'none' : '3,3'}
              opacity="0.8"
            />
          ))}
        </svg>

        {/* Incident Dots */}
        {activeIncidents.map(inc => (
          <div
            key={inc.id}
            className="absolute"
            style={{ left: `${inc.coordinates.x}%`, top: `${inc.coordinates.y}%`, transform: 'translate(-50%,-50%)' }}
            title={`${inc.type} — ${inc.location}`}
          >
            <div className={`
              w-4 h-4 rounded-full border-2 flex items-center justify-center
              ${inc.severity_level === 'Critical' ? 'bg-crisis-red border-white' : 'bg-crisis-orange border-white'}
            `}>
              <div className="map-dot-critical absolute w-4 h-4 rounded-full bg-crisis-red/50" />
            </div>
          </div>
        ))}

        {/* Legend */}
        <div className="absolute bottom-1 right-1 flex flex-col gap-0.5">
          <div className="flex items-center gap-1">
            <div className="w-2 h-2 rounded-full bg-crisis-red" />
            <span className="text-[7px] font-mono text-crisis-muted">INCIDENT</span>
          </div>
          <div className="flex items-center gap-1">
            <div className="w-4 border-t-2 border-crisis-green" />
            <span className="text-[7px] font-mono text-crisis-muted">EVAC</span>
          </div>
        </div>
      </div>

      {/* Navigation hint */}
      <div className="mt-2 flex items-center gap-1 text-[9px] font-mono text-crisis-cyan">
        <Navigation size={9} />
        <span>Dynamic routes updating — 2 active evac paths</span>
      </div>
    </div>
  );
}
```

### `src/components/dashboard/EvacuationProgress.jsx`

```jsx
import { useCrisis } from '../../context/CrisisContext';
import { ShieldAlert } from 'lucide-react';

export function EvacuationProgress() {
  const { incidents } = useCrisis();
  const active = incidents.filter(i => i.status !== 'Resolved' && i.evacuation_progress > 0);

  return (
    <div className="p-3 border-b border-crisis-border">
      <div className="flex items-center gap-2 mb-3">
        <ShieldAlert size={13} className="text-crisis-orange" />
        <span className="font-display text-[11px] tracking-widest text-crisis-text font-semibold">EVACUATION STATUS</span>
      </div>
      <div className="space-y-3">
        {active.map(inc => (
          <div key={inc.id}>
            <div className="flex justify-between items-center mb-1">
              <span className="text-crisis-text text-[10px] font-mono truncate flex-1">{inc.type} — {inc.location.split('—')[0]}</span>
              <span className={`text-[10px] font-mono font-bold ml-2 ${inc.evacuation_progress === 100 ? 'text-crisis-green' : 'text-crisis-orange'}`}>
                {inc.evacuation_progress}%
              </span>
            </div>
            <div className="h-1.5 bg-crisis-bg rounded-full overflow-hidden border border-crisis-border">
              <div
                className={`h-full rounded-full transition-all duration-1000 ${
                  inc.evacuation_progress === 100 ? 'bg-crisis-green' :
                  inc.evacuation_progress > 60 ? 'bg-crisis-yellow' : 'bg-crisis-orange'
                }`}
                style={{ width: `${inc.evacuation_progress}%` }}
              />
            </div>
          </div>
        ))}
        {active.length === 0 && (
          <p className="text-crisis-muted text-[10px] font-mono text-center py-2">No active evacuations</p>
        )}
      </div>
    </div>
  );
}
```

### `src/components/dashboard/AlertsBroadcast.jsx`

```jsx
import { useCrisis } from '../../context/CrisisContext';
import { Megaphone, MessageSquare, Bell, Smartphone } from 'lucide-react';

const CHANNELS = [
  { icon: Megaphone,   label: 'PA System',       active: true,  count: '12 zones' },
  { icon: Smartphone,  label: 'Guest App Push',   active: true,  count: '243 guests' },
  { icon: MessageSquare, label: 'Staff SMS',      active: true,  count: '8 staff' },
  { icon: Bell,        label: 'Emergency Services', active: false, count: 'Not sent' },
];

export function AlertsBroadcast() {
  const { setShowBroadcast, setBroadcastTarget } = useCrisis();

  return (
    <div className="p-3">
      <div className="flex items-center gap-2 mb-3">
        <Megaphone size={13} className="text-crisis-cyan" />
        <span className="font-display text-[11px] tracking-widest text-crisis-text font-semibold">BROADCAST CHANNELS</span>
      </div>
      <div className="space-y-2">
        {CHANNELS.map(({ icon: Icon, label, active, count }) => (
          <div key={label} className={`flex items-center justify-between p-2 rounded border ${active ? 'border-crisis-green/30 bg-green-950/20' : 'border-crisis-border bg-crisis-card/30'}`}>
            <div className="flex items-center gap-2">
              <Icon size={11} className={active ? 'text-crisis-green' : 'text-crisis-muted'} />
              <span className={`text-[10px] font-medium ${active ? 'text-crisis-text' : 'text-crisis-muted'}`}>{label}</span>
            </div>
            <div className="flex items-center gap-2">
              <span className="text-[9px] font-mono text-crisis-muted">{count}</span>
              <div className={`w-1.5 h-1.5 rounded-full ${active ? 'bg-crisis-green' : 'bg-crisis-muted'}`} />
            </div>
          </div>
        ))}
      </div>
      <button
        onClick={() => { setBroadcastTarget(null); setShowBroadcast(true); }}
        className="mt-3 w-full py-2 rounded border border-crisis-cyan/40 bg-crisis-cyan/10 text-crisis-cyan text-xs font-bold font-mono tracking-widest hover:bg-crisis-cyan/20 transition-all"
      >
        + BROADCAST ALL CHANNELS
      </button>
    </div>
  );
}
```

---

## 7. Modals

### `src/components/modals/BroadcastModal.jsx`

```jsx
import { motion, AnimatePresence } from 'framer-motion';
import { useCrisis } from '../../context/CrisisContext';
import { X, Radio, Send, Volume2, Smartphone, MessageSquare, Mail } from 'lucide-react';
import { useState } from 'react';

const CHANNELS = [
  { id: 'pa',    icon: Volume2,        label: 'PA System',        desc: 'All hotel floors' },
  { id: 'push',  icon: Smartphone,     label: 'Guest App Push',   desc: '243 active guests' },
  { id: 'sms',   icon: MessageSquare,  label: 'Staff SMS',        desc: '8 on-duty staff' },
  { id: 'email', icon: Mail,           label: 'Management Email', desc: 'GM & Department Heads' },
];

export function BroadcastModal() {
  const { showBroadcast, setShowBroadcast, broadcastTarget, pushNotification } = useCrisis();
  const [selected, setSelected]   = useState(['pa', 'push', 'sms']);
  const [message, setMessage]     = useState(broadcastTarget
    ? `EMERGENCY ALERT — ${broadcastTarget.type} detected at ${broadcastTarget.location}. Please follow staff instructions and proceed to nearest exit. This is NOT a drill.`
    : '');
  const [sending, setSending]     = useState(false);
  const [sent, setSent]           = useState(false);

  const toggle = (id) => setSelected(prev =>
    prev.includes(id) ? prev.filter(x => x !== id) : [...prev, id]
  );

  const handleSend = async () => {
    setSending(true);
    await new Promise(r => setTimeout(r, 1800));
    setSending(false);
    setSent(true);
    pushNotification(`📣 Broadcast sent via ${selected.join(', ')} — ${selected.length} channels`, 'success');
    setTimeout(() => { setSent(false); setShowBroadcast(false); }, 2000);
  };

  return (
    <AnimatePresence>
      {showBroadcast && (
        <motion.div
          initial={{ opacity: 0 }}
          animate={{ opacity: 1 }}
          exit={{ opacity: 0 }}
          className="fixed inset-0 bg-black/80 backdrop-blur-sm flex items-center justify-center z-[100] p-4"
          onClick={e => e.target === e.currentTarget && setShowBroadcast(false)}
        >
          <motion.div
            initial={{ scale: 0.9, y: 20 }}
            animate={{ scale: 1, y: 0 }}
            exit={{ scale: 0.9, y: 20 }}
            className="bg-crisis-surface border border-crisis-border rounded-xl w-full max-w-lg shadow-[0_0_60px_rgba(0,245,255,0.1)]"
          >
            {/* Header */}
            <div className="flex items-center justify-between p-5 border-b border-crisis-border">
              <div className="flex items-center gap-3">
                <div className="w-10 h-10 rounded-lg bg-crisis-red/20 border border-crisis-red/40 flex items-center justify-center">
                  <Radio size={20} className="text-crisis-red" />
                </div>
                <div>
                  <h2 className="font-display font-bold text-sm text-white">EMERGENCY BROADCAST</h2>
                  <p className="text-crisis-muted text-[10px] font-mono">
                    {broadcastTarget ? `For: ${broadcastTarget.id}` : 'General broadcast — all zones'}
                  </p>
                </div>
              </div>
              <button onClick={() => setShowBroadcast(false)} className="text-crisis-muted hover:text-white transition-colors">
                <X size={18} />
              </button>
            </div>

            <div className="p-5 space-y-5">
              {/* Message */}
              <div>
                <label className="text-crisis-muted text-[10px] font-mono tracking-widest block mb-2">MESSAGE CONTENT</label>
                <textarea
                  value={message}
                  onChange={e => setMessage(e.target.value)}
                  rows={4}
                  className="w-full bg-crisis-bg border border-crisis-border rounded-lg p-3 text-crisis-text text-sm font-mono resize-none focus:outline-none focus:border-crisis-cyan/60"
                />
              </div>

              {/* Channels */}
              <div>
                <label className="text-crisis-muted text-[10px] font-mono tracking-widest block mb-2">BROADCAST CHANNELS</label>
                <div className="grid grid-cols-2 gap-2">
                  {CHANNELS.map(({ id, icon: Icon, label, desc }) => (
                    <button
                      key={id}
                      onClick={() => toggle(id)}
                      className={`
                        p-3 rounded-lg border text-left transition-all
                        ${selected.includes(id)
                          ? 'bg-crisis-cyan/10 border-crisis-cyan/50 text-crisis-text'
                          : 'bg-crisis-card border-crisis-border text-crisis-muted hover:border-crisis-muted'
                        }
                      `}
                    >
                      <div className="flex items-center gap-2 mb-1">
                        <Icon size={13} className={selected.includes(id) ? 'text-crisis-cyan' : 'text-crisis-muted'} />
                        <span className="text-xs font-semibold">{label}</span>
                      </div>
                      <p className="text-[9px] font-mono">{desc}</p>
                    </button>
                  ))}
                </div>
              </div>

              {/* Send Button */}
              <button
                onClick={handleSend}
                disabled={sending || sent || !message || selected.length === 0}
                className={`
                  w-full py-3 rounded-lg font-bold text-sm font-display tracking-widest
                  flex items-center justify-center gap-2 transition-all
                  ${sent ? 'bg-crisis-green text-black'
                    : sending ? 'bg-crisis-orange/50 text-crisis-orange cursor-wait'
                    : 'bg-crisis-red text-white hover:bg-red-600 shadow-[0_0_20px_rgba(255,26,26,0.4)] hover:shadow-[0_0_30px_rgba(255,26,26,0.6)]'
                  }
                `}
              >
                {sent ? '✓ BROADCAST SENT' : sending ? (
                  <>
                    <div className="w-4 h-4 border-2 border-current border-t-transparent rounded-full animate-spin" />
                    TRANSMITTING…
                  </>
                ) : (
                  <>
                    <Send size={14} />
                    SEND BROADCAST NOW
                  </>
                )}
              </button>
            </div>
          </motion.div>
        </motion.div>
      )}
    </AnimatePresence>
  );
}
```

### `src/components/modals/EscalateModal.jsx`

```jsx
import { motion, AnimatePresence } from 'framer-motion';
import { useCrisis } from '../../context/CrisisContext';
import { X, PhoneCall, AlertTriangle } from 'lucide-react';
import { useState } from 'react';

const SERVICES = [
  { id: '100', label: 'Police', icon: '🚔', number: '100' },
  { id: '101', label: 'Fire Brigade', icon: '🚒', number: '101' },
  { id: '108', label: 'Ambulance / EMRI', icon: '🚑', number: '108' },
  { id: '1091', label: 'Women Helpline', icon: '🛡️', number: '1091' },
  { id: '1070', label: 'Disaster Mgmt', icon: '⛑️', number: '1070' },
];

export function EscalateModal() {
  const { showEscalate, setShowEscalate, activeIncident, pushNotification } = useCrisis();
  const [calling, setCalling]   = useState(null);
  const [called, setCalled]     = useState([]);

  const handleCall = (service) => {
    setCalling(service.id);
    setTimeout(() => {
      setCalling(null);
      setCalled(prev => [...prev, service.id]);
      pushNotification(`📞 ${service.label} (${service.number}) notified`, 'success');
    }, 2000);
  };

  return (
    <AnimatePresence>
      {showEscalate && (
        <motion.div
          initial={{ opacity: 0 }}
          animate={{ opacity: 1 }}
          exit={{ opacity: 0 }}
          className="fixed inset-0 bg-black/80 backdrop-blur-sm flex items-center justify-center z-[100] p-4"
          onClick={e => e.target === e.currentTarget && setShowEscalate(false)}
        >
          <motion.div
            initial={{ scale: 0.9, y: 20 }}
            animate={{ scale: 1, y: 0 }}
            exit={{ scale: 0.9, y: 20 }}
            className="bg-crisis-surface border border-crisis-red/50 rounded-xl w-full max-w-md shadow-[0_0_60px_rgba(255,26,26,0.2)]"
          >
            <div className="flex items-center justify-between p-5 border-b border-crisis-border">
              <div className="flex items-center gap-3">
                <AlertTriangle size={20} className="text-crisis-red animate-pulse" />
                <div>
                  <h2 className="font-display font-bold text-sm text-white">ESCALATE TO EMERGENCY SERVICES</h2>
                  {activeIncident && (
                    <p className="text-crisis-red text-[10px] font-mono">{activeIncident.id} — {activeIncident.type}</p>
                  )}
                </div>
              </div>
              <button onClick={() => setShowEscalate(false)} className="text-crisis-muted hover:text-white">
                <X size={18} />
              </button>
            </div>

            <div className="p-5">
              <p className="text-crisis-muted text-xs mb-4 font-mono">
                All calls are recorded and logged automatically. Location and incident details will be transmitted.
              </p>
              <div className="space-y-2">
                {SERVICES.map(service => (
                  <button
                    key={service.id}
                    onClick={() => !called.includes(service.id) && handleCall(service)}
                    disabled={called.includes(service.id)}
                    className={`
                      w-full flex items-center justify-between p-3 rounded-lg border transition-all
                      ${called.includes(service.id)
                        ? 'border-crisis-green/50 bg-green-950/30 text-crisis-green cursor-default'
                        : calling === service.id
                        ? 'border-crisis-yellow/50 bg-yellow-950/30 text-crisis-yellow cursor-wait'
                        : 'border-crisis-border hover:border-crisis-red/50 hover:bg-red-950/20 text-crisis-text'
                      }
                    `}
                  >
                    <div className="flex items-center gap-3">
                      <span className="text-xl">{service.icon}</span>
                      <div className="text-left">
                        <p className="font-semibold text-sm">{service.label}</p>
                        <p className="font-mono text-[11px] opacity-70">National: {service.number}</p>
                      </div>
                    </div>
                    <div className="flex items-center gap-2">
                      {called.includes(service.id) ? (
                        <span className="text-xs font-mono text-crisis-green">NOTIFIED ✓</span>
                      ) : calling === service.id ? (
                        <div className="w-4 h-4 border-2 border-current border-t-transparent rounded-full animate-spin" />
                      ) : (
                        <PhoneCall size={14} className="text-crisis-red" />
                      )}
                    </div>
                  </button>
                ))}
              </div>
            </div>
          </motion.div>
        </motion.div>
      )}
    </AnimatePresence>
  );
}
```

---

## 8. Pages

### `src/pages/Login.jsx`

```jsx
import { useState } from 'react';
import { useNavigate } from 'react-router-dom';
import { motion } from 'framer-motion';
import { Shield, Eye, EyeOff, AlertTriangle, ChevronRight } from 'lucide-react';

const ROLES = [
  { id: 'manager',   label: 'Hotel Manager',     icon: '🏨', color: 'text-crisis-cyan',   border: 'border-crisis-cyan/40',  bg: 'bg-crisis-cyan/10'  },
  { id: 'admin',     label: 'System Admin',       icon: '⚙️', color: 'text-crisis-orange', border: 'border-crisis-orange/40', bg: 'bg-crisis-orange/10' },
  { id: 'hospital',  label: 'Hospital / Medical', icon: '🏥', color: 'text-crisis-green',  border: 'border-crisis-green/40',  bg: 'bg-crisis-green/10'  },
  { id: 'security',  label: 'Security Officer',   icon: '🛡️', color: 'text-purple-400',    border: 'border-purple-400/40',    bg: 'bg-purple-950/30'    },
  { id: 'responder', label: 'Emergency Responder',icon: '🚨', color: 'text-crisis-red',    border: 'border-crisis-red/40',    bg: 'bg-red-950/30'       },
  { id: 'staff',     label: 'Hotel Staff',        icon: '👤', color: 'text-crisis-text',   border: 'border-crisis-border',    bg: 'bg-crisis-card'      },
];

export function Login({ onLogin }) {
  const [selectedRole, setSelectedRole] = useState('manager');
  const [email, setEmail]               = useState('');
  const [password, setPassword]         = useState('');
  const [showPwd, setShowPwd]           = useState(false);
  const [loading, setLoading]           = useState(false);
  const [error, setError]               = useState('');
  const navigate = useNavigate();

  const handleLogin = async (e) => {
    e.preventDefault();
    if (!email || !password) { setError('Please enter credentials'); return; }
    setLoading(true);
    setError('');
    await new Promise(r => setTimeout(r, 1500));
    setLoading(false);
    const role = ROLES.find(r => r.id === selectedRole);
    onLogin({ name: email.split('@')[0] || 'Operator', role: role?.label || 'Staff', avatar: email.slice(0,2).toUpperCase(), roleId: selectedRole });
    navigate('/dashboard');
  };

  const selectedRoleObj = ROLES.find(r => r.id === selectedRole);

  return (
    <div className="min-h-screen hex-bg flex items-center justify-center p-4 relative overflow-hidden">
      {/* Animated scan line */}
      <div className="pointer-events-none absolute inset-0 overflow-hidden">
        <div className="absolute top-0 left-0 right-0 h-px bg-gradient-to-r from-transparent via-crisis-cyan/30 to-transparent animate-scan-line" />
      </div>

      {/* Background alert */}
      <div className="absolute top-4 left-0 right-0 flex justify-center">
        <div className="flex items-center gap-2 bg-red-950/80 border border-crisis-red/50 rounded-lg px-4 py-2 backdrop-blur">
          <AlertTriangle size={14} className="text-crisis-red animate-pulse" />
          <span className="text-crisis-red text-xs font-mono font-bold">LIVE — 3 ACTIVE INCIDENTS | GRAND HYATT BENGALURU</span>
        </div>
      </div>

      <motion.div
        initial={{ opacity: 0, y: 30 }}
        animate={{ opacity: 1, y: 0 }}
        transition={{ duration: 0.6, ease: [0.16, 1, 0.3, 1] }}
        className="w-full max-w-md"
      >
        {/* Logo */}
        <div className="text-center mb-8">
          <motion.div
            initial={{ scale: 0.5, opacity: 0 }}
            animate={{ scale: 1, opacity: 1 }}
            transition={{ delay: 0.2, duration: 0.5, type: 'spring' }}
            className="inline-flex items-center justify-center w-20 h-20 rounded-2xl bg-crisis-surface border border-crisis-cyan/30 mb-4 shadow-[0_0_40px_rgba(0,245,255,0.2)]"
          >
            <Shield size={40} className="text-crisis-cyan animate-glow-pulse" />
          </motion.div>
          <h1 className="font-display font-black text-2xl text-white glow-cyan tracking-widest">CRISISSYNC AI</h1>
          <p className="text-crisis-muted text-xs font-mono mt-1 tracking-widest">RAPID CRISIS RESPONSE PLATFORM v2.4</p>
          <p className="text-crisis-muted text-[10px] font-mono mt-0.5">Grand Hyatt Bengaluru | Emergency Operations</p>
        </div>

        {/* Card */}
        <div className="bg-crisis-surface border border-crisis-border rounded-2xl p-6 shadow-[0_0_60px_rgba(0,0,0,0.5)] backdrop-blur">

          {/* Role Grid */}
          <div className="mb-5">
            <p className="text-crisis-muted text-[10px] font-mono tracking-widest mb-3">SELECT ROLE</p>
            <div className="grid grid-cols-3 gap-2">
              {ROLES.map(role => (
                <button
                  key={role.id}
                  onClick={() => setSelectedRole(role.id)}
                  className={`
                    p-2 rounded-lg border text-center transition-all duration-200
                    ${selectedRole === role.id ? `${role.border} ${role.bg}` : 'border-crisis-border bg-crisis-card hover:border-crisis-muted'}
                  `}
                >
                  <div className="text-xl mb-1">{role.icon}</div>
                  <p className={`text-[9px] font-semibold leading-tight ${selectedRole === role.id ? role.color : 'text-crisis-muted'}`}>
                    {role.label}
                  </p>
                </button>
              ))}
            </div>
          </div>

          {/* Form */}
          <form onSubmit={handleLogin} className="space-y-4">
            <div>
              <label className="text-crisis-muted text-[10px] font-mono tracking-widest block mb-1.5">EMAIL / STAFF ID</label>
              <input
                type="text"
                value={email}
                onChange={e => setEmail(e.target.value)}
                placeholder="officer@grandhyatt.com"
                className="w-full bg-crisis-bg border border-crisis-border rounded-lg px-4 py-3 text-crisis-text text-sm font-mono placeholder-crisis-muted/50 focus:outline-none focus:border-crisis-cyan/60 transition-colors"
              />
            </div>

            <div>
              <label className="text-crisis-muted text-[10px] font-mono tracking-widest block mb-1.5">PASSWORD / BADGE PIN</label>
              <div className="relative">
                <input
                  type={showPwd ? 'text' : 'password'}
                  value={password}
                  onChange={e => setPassword(e.target.value)}
                  placeholder="••••••••"
                  className="w-full bg-crisis-bg border border-crisis-border rounded-lg px-4 py-3 pr-11 text-crisis-text text-sm font-mono placeholder-crisis-muted/50 focus:outline-none focus:border-crisis-cyan/60 transition-colors"
                />
                <button
                  type="button"
                  onClick={() => setShowPwd(v => !v)}
                  className="absolute right-3 top-1/2 -translate-y-1/2 text-crisis-muted hover:text-crisis-text"
                >
                  {showPwd ? <EyeOff size={16} /> : <Eye size={16} />}
                </button>
              </div>
            </div>

            {error && (
              <p className="text-crisis-red text-xs font-mono flex items-center gap-1">
                <AlertTriangle size={12} /> {error}
              </p>
            )}

            <button
              type="submit"
              disabled={loading}
              className={`
                w-full py-3 rounded-lg font-display font-bold text-sm tracking-widest
                flex items-center justify-center gap-2 transition-all duration-300
                ${loading
                  ? 'bg-crisis-muted/30 text-crisis-muted cursor-wait'
                  : `${selectedRoleObj?.bg || 'bg-crisis-cyan/10'} ${selectedRoleObj?.color || 'text-crisis-cyan'} ${selectedRoleObj?.border || 'border-crisis-cyan/40'} border hover:brightness-125 shadow-lg`
                }
              `}
            >
              {loading ? (
                <>
                  <div className="w-4 h-4 border-2 border-current border-t-transparent rounded-full animate-spin" />
                  AUTHENTICATING…
                </>
              ) : (
                <>
                  ACCESS CONTROL ROOM
                  <ChevronRight size={16} />
                </>
              )}
            </button>
          </form>

          <div className="mt-4 pt-4 border-t border-crisis-border flex items-center justify-between">
            <p className="text-crisis-muted text-[10px] font-mono">🔒 256-bit AES encrypted</p>
            <p className="text-crisis-muted text-[10px] font-mono">All access logged</p>
          </div>
        </div>
      </motion.div>
    </div>
  );
}
```

### `src/pages/Dashboard.jsx`

```jsx
import { useCrisis } from '../context/CrisisContext';
import { Sidebar }      from '../components/layout/Sidebar';
import { RightPanel }   from '../components/layout/RightPanel';
import { IncidentCard } from '../components/dashboard/IncidentCard';
import { BroadcastModal } from '../components/modals/BroadcastModal';
import { EscalateModal }  from '../components/modals/EscalateModal';
import { AnimatePresence, motion } from 'framer-motion';
import { Filter, RefreshCw } from 'lucide-react';
import { useState } from 'react';

const FILTERS = ['All', 'Critical', 'High', 'Active', 'Resolved'];

export function Dashboard() {
  const { incidents, notifications, alarmActive } = useCrisis();
  const [filter, setFilter] = useState('All');
  const [sortBy, setSortBy] = useState('time');

  const filtered = incidents
    .filter(i => {
      if (filter === 'All')      return true;
      if (filter === 'Active')   return i.status === 'Active' || i.status === 'New';
      if (filter === 'Resolved') return i.status === 'Resolved';
      return i.severity_level === filter;
    })
    .sort((a, b) => {
      if (sortBy === 'time')     return new Date(b.timestamp) - new Date(a.timestamp);
      if (sortBy === 'severity') {
        const order = { Critical: 0, High: 1, Medium: 2, Low: 3 };
        return (order[a.severity_level] ?? 9) - (order[b.severity_level] ?? 9);
      }
      return 0;
    });

  return (
    <div className={`flex flex-1 overflow-hidden ${alarmActive ? 'animate-flicker' : ''}`}>
      <Sidebar />

      {/* Main Feed */}
      <main className="flex-1 overflow-y-auto bg-crisis-bg bg-grid-pattern bg-grid relative">
        {/* Toolbar */}
        <div className="sticky top-0 z-10 bg-crisis-bg/90 backdrop-blur border-b border-crisis-border px-4 py-2.5 flex items-center justify-between gap-3">
          <div className="flex items-center gap-2">
            <Filter size={13} className="text-crisis-cyan" />
            <div className="flex gap-1">
              {FILTERS.map(f => (
                <button
                  key={f}
                  onClick={() => setFilter(f)}
                  className={`
                    px-2.5 py-1 rounded text-[10px] font-mono font-semibold tracking-widest transition-all
                    ${filter === f
                      ? 'bg-crisis-cyan/20 text-crisis-cyan border border-crisis-cyan/40'
                      : 'text-crisis-muted hover:text-crisis-text'
                    }
                  `}
                >
                  {f}
                </button>
              ))}
            </div>
          </div>

          <div className="flex items-center gap-3">
            <select
              value={sortBy}
              onChange={e => setSortBy(e.target.value)}
              className="bg-crisis-card border border-crisis-border rounded px-2 py-1 text-crisis-muted text-[10px] font-mono focus:outline-none"
            >
              <option value="time">Sort: Latest</option>
              <option value="severity">Sort: Severity</option>
            </select>
            <div className="flex items-center gap-1.5 text-crisis-green text-[10px] font-mono">
              <RefreshCw size={10} className="animate-spin" />
              LIVE
            </div>
          </div>
        </div>

        {/* Incident Cards */}
        <div className="p-4 space-y-3 max-w-3xl mx-auto">
          <AnimatePresence mode="popLayout">
            {filtered.map(incident => (
              <IncidentCard key={incident.id} incident={incident} />
            ))}
          </AnimatePresence>

          {filtered.length === 0 && (
            <div className="text-center py-20">
              <p className="text-crisis-muted font-mono text-sm">No incidents match this filter</p>
            </div>
          )}
        </div>
      </main>

      <RightPanel />

      {/* Notifications Toast */}
      <div className="fixed bottom-4 right-4 space-y-2 z-50 w-80">
        <AnimatePresence>
          {notifications.map(n => (
            <motion.div
              key={n.id}
              initial={{ opacity: 0, x: 60 }}
              animate={{ opacity: 1, x: 0 }}
              exit={{ opacity: 0, x: 60 }}
              className={`
                p-3 rounded-lg border backdrop-blur text-sm font-mono
                ${n.type === 'critical' ? 'bg-red-950/90 border-crisis-red text-crisis-red' :
                  n.type === 'success'  ? 'bg-green-950/90 border-crisis-green text-crisis-green' :
                  n.type === 'warning'  ? 'bg-orange-950/90 border-crisis-orange text-crisis-orange' :
                  'bg-crisis-surface/90 border-crisis-border text-crisis-text'}
              `}
            >
              {n.message}
            </motion.div>
          ))}
        </AnimatePresence>
      </div>

      {/* Alarm Flash Overlay */}
      <AnimatePresence>
        {alarmActive && (
          <motion.div
            initial={{ opacity: 0 }}
            animate={{ opacity: [0, 0.15, 0, 0.15, 0] }}
            exit={{ opacity: 0 }}
            transition={{ duration: 1, repeat: 5 }}
            className="fixed inset-0 bg-crisis-red pointer-events-none z-40"
          />
        )}
      </AnimatePresence>

      <BroadcastModal />
      <EscalateModal />
    </div>
  );
}
```

### `src/pages/IncidentLog.jsx`

```jsx
import { useCrisis } from '../context/CrisisContext';
import { StatusBadge } from '../components/ui/StatusBadge';
import { formatDistanceToNow } from 'date-fns';
import { Download, FileText } from 'lucide-react';

export function IncidentLog() {
  const { incidents } = useCrisis();

  const handleExport = () => {
    const csv = [
      ['ID', 'Type', 'Location', 'Severity', 'Status', 'Time', 'Guests Affected'].join(','),
      ...incidents.map(i => [i.id, i.type, `"${i.location}"`, i.severity_level, i.status, i.timestamp, i.guest_count_affected].join(',')),
    ].join('\n');
    const blob = new Blob([csv], { type: 'text/csv' });
    const url = URL.createObjectURL(blob);
    const a = document.createElement('a'); a.href = url; a.download = 'incident_log.csv'; a.click();
  };

  return (
    <div className="flex-1 overflow-y-auto bg-crisis-bg p-6">
      <div className="max-w-5xl mx-auto">
        <div className="flex items-center justify-between mb-6">
          <div className="flex items-center gap-3">
            <FileText size={20} className="text-crisis-cyan" />
            <h1 className="font-display font-bold text-white text-lg tracking-widest">INCIDENT LOG</h1>
            <span className="text-crisis-muted font-mono text-xs">— {incidents.length} total records</span>
          </div>
          <button
            onClick={handleExport}
            className="flex items-center gap-2 px-4 py-2 rounded border border-crisis-cyan/40 bg-crisis-cyan/10 text-crisis-cyan text-xs font-mono hover:bg-crisis-cyan/20 transition-all"
          >
            <Download size={13} />
            EXPORT CSV
          </button>
        </div>

        <div className="bg-crisis-surface border border-crisis-border rounded-xl overflow-hidden">
          <table className="w-full">
            <thead>
              <tr className="border-b border-crisis-border">
                {['ID', 'TYPE', 'LOCATION', 'SEVERITY', 'STATUS', 'TIME', 'GUESTS', 'EVAC %'].map(h => (
                  <th key={h} className="text-left px-4 py-3 text-[10px] font-mono font-semibold text-crisis-muted tracking-widest">{h}</th>
                ))}
              </tr>
            </thead>
            <tbody>
              {incidents.map((inc, i) => (
                <tr
                  key={inc.id}
                  className={`border-b border-crisis-border/50 hover:bg-crisis-card/50 transition-colors ${inc.severity_level === 'Critical' && inc.status !== 'Resolved' ? 'bg-red-950/10' : ''}`}
                >
                  <td className="px-4 py-3 text-crisis-cyan text-xs font-mono">{inc.id}</td>
                  <td className="px-4 py-3 text-crisis-text text-xs font-medium">{inc.type}</td>
                  <td className="px-4 py-3 text-crisis-text text-xs max-w-[160px] truncate">{inc.location}</td>
                  <td className="px-4 py-3"><StatusBadge status={inc.severity_level} /></td>
                  <td className="px-4 py-3"><StatusBadge status={inc.status} /></td>
                  <td className="px-4 py-3 text-crisis-muted text-[10px] font-mono">{formatDistanceToNow(new Date(inc.timestamp), { addSuffix: true })}</td>
                  <td className="px-4 py-3 text-crisis-text text-xs font-mono text-center">{inc.guest_count_affected}</td>
                  <td className="px-4 py-3">
                    <div className="flex items-center gap-2">
                      <div className="flex-1 h-1.5 bg-crisis-bg rounded-full border border-crisis-border overflow-hidden" style={{ width: 50 }}>
                        <div
                          className={`h-full rounded-full ${inc.evacuation_progress === 100 ? 'bg-crisis-green' : 'bg-crisis-orange'}`}
                          style={{ width: `${inc.evacuation_progress}%` }}
                        />
                      </div>
                      <span className="text-[10px] font-mono text-crisis-muted">{inc.evacuation_progress}%</span>
                    </div>
                  </td>
                </tr>
              ))}
            </tbody>
          </table>
        </div>
      </div>
    </div>
  );
}
```

### `src/pages/DigitalTwin.jsx`

```jsx
import { useCrisis } from '../context/CrisisContext';
import { PROPERTY_ZONES, EVAC_ROUTES } from '../data/mapData';
import { Layers, ZoomIn, ZoomOut } from 'lucide-react';
import { useState } from 'react';
import { StatusBadge } from '../components/ui/StatusBadge';

export function DigitalTwin() {
  const { incidents, staff } = useCrisis();
  const [scale, setScale] = useState(1);
  const [selectedFloor, setSelectedFloor] = useState('all');

  const floors = ['all', '12', '5', '2', '1', 'B1', 'P2'];
  const activeIncidents = incidents.filter(i => i.status !== 'Resolved');

  return (
    <div className="flex-1 overflow-y-auto bg-crisis-bg p-6">
      <div className="max-w-6xl mx-auto">
        <div className="flex items-center justify-between mb-6">
          <div className="flex items-center gap-3">
            <Layers size={20} className="text-crisis-cyan" />
            <h1 className="font-display font-bold text-white text-lg tracking-widest">DIGITAL TWIN — LIVE PROPERTY VIEW</h1>
          </div>
          <div className="flex items-center gap-2">
            {floors.map(f => (
              <button
                key={f}
                onClick={() => setSelectedFloor(f)}
                className={`px-2.5 py-1 rounded text-[10px] font-mono font-semibold transition-all
                  ${selectedFloor === f ? 'bg-crisis-cyan/20 text-crisis-cyan border border-crisis-cyan/40' : 'text-crisis-muted hover:text-crisis-text'}`}
              >
                {f === 'all' ? 'ALL' : `L${f}`}
              </button>
            ))}
            <div className="flex gap-1 ml-2">
              <button onClick={() => setScale(s => Math.min(2, s + 0.2))} className="p-1.5 rounded bg-crisis-card border border-crisis-border text-crisis-muted hover:text-crisis-text transition-colors"><ZoomIn size={13} /></button>
              <button onClick={() => setScale(s => Math.max(0.5, s - 0.2))} className="p-1.5 rounded bg-crisis-card border border-crisis-border text-crisis-muted hover:text-crisis-text transition-colors"><ZoomOut size={13} /></button>
            </div>
          </div>
        </div>

        <div className="grid grid-cols-3 gap-4">
          {/* Map */}
          <div className="col-span-2">
            <div className="bg-crisis-surface border border-crisis-border rounded-xl p-4">
              <div
                className="relative overflow-hidden rounded-lg bg-crisis-bg border border-crisis-border"
                style={{ height: 480, transition: 'transform 0.3s', transform: `scale(${scale})`, transformOrigin: 'top left' }}
              >
                {/* Grid */}
                <div className="absolute inset-0" style={{ backgroundImage: 'linear-gradient(rgba(0,245,255,0.04) 1px, transparent 1px), linear-gradient(90deg, rgba(0,245,255,0.04) 1px, transparent 1px)', backgroundSize: '5% 5%' }} />

                {/* Zones */}
                {PROPERTY_ZONES.map(zone => (
                  <div
                    key={zone.id}
                    className="absolute rounded border border-crisis-border/70 flex items-center justify-center transition-all hover:brightness-125 cursor-pointer"
                    style={{ left: `${zone.x}%`, top: `${zone.y}%`, width: `${zone.w}%`, height: `${zone.h}%`, background: zone.color }}
                  >
                    <span className="text-[8px] font-mono text-crisis-muted text-center leading-tight px-1">{zone.label}</span>
                  </div>
                ))}

                {/* Evac Routes */}
                <svg className="absolute inset-0 w-full h-full pointer-events-none">
                  <defs>
                    <marker id="arrowGreen" markerWidth="6" markerHeight="6" refX="3" refY="3" orient="auto">
                      <path d="M0,0 L0,6 L6,3 z" fill="#00FF88" />
                    </marker>
                    <marker id="arrowRed" markerWidth="6" markerHeight="6" refX="3" refY="3" orient="auto">
                      <path d="M0,0 L0,6 L6,3 z" fill="#FF1A1A" />
                    </marker>
                  </defs>
                  {EVAC_ROUTES.map((route, i) => (
                    <line
                      key={i}
                      x1={`${route.from.x}%`} y1={`${route.from.y}%`}
                      x2={`${route.to.x}%`}   y2={`${route.to.y}%`}
                      stroke={route.active ? '#00FF88' : '#FF1A1A'}
                      strokeWidth="2"
                      strokeDasharray={route.active ? 'none' : '4,4'}
                      markerEnd={route.active ? 'url(#arrowGreen)' : 'url(#arrowRed)'}
                      opacity="0.9"
                    />
                  ))}
                </svg>

                {/* Incident Markers */}
                {activeIncidents.map(inc => (
                  <div
                    key={inc.id}
                    className="absolute"
                    style={{ left: `${inc.coordinates.x}%`, top: `${inc.coordinates.y}%`, transform: 'translate(-50%,-50%)' }}
                    title={`${inc.type} — ${inc.location}`}
                  >
                    <div className={`relative w-6 h-6 rounded-full border-2 border-white flex items-center justify-center text-xs
                      ${inc.severity_level === 'Critical' ? 'bg-crisis-red animate-pulse-red' : 'bg-crisis-orange'}`}>
                      <span>!</span>
                      <div className="absolute inset-0 rounded-full bg-current opacity-30 animate-ping" />
                    </div>
                  </div>
                ))}

                {/* Staff positions */}
                {staff.filter(s => s.responding).map((member, i) => {
                  const zone = PROPERTY_ZONES.find(z => z.id.includes(member.zone.split('-')[0]));
                  if (!zone) return null;
                  return (
                    <div
                      key={member.id}
                      className="absolute w-5 h-5 rounded-full bg-crisis-cyan/30 border border-crisis-cyan flex items-center justify-center text-[8px] font-bold text-crisis-cyan"
                      style={{ left: `${zone.x + 5 + i * 3}%`, top: `${zone.y + 3}%`, transform: 'translate(-50%,-50%)' }}
                      title={member.name}
                    >
                      {member.avatar}
                    </div>
                  );
                })}
              </div>
            </div>
          </div>

          {/* Right Stats */}
          <div className="space-y-3">
            <div className="bg-crisis-surface border border-crisis-border rounded-xl p-4">
              <h3 className="font-display text-[11px] tracking-widest text-crisis-text font-semibold mb-3">INCIDENT OVERLAY</h3>
              <div className="space-y-2">
                {activeIncidents.map(inc => (
                  <div key={inc.id} className={`p-2 rounded border ${inc.severity_level === 'Critical' ? 'border-crisis-red/50 bg-red-950/20' : 'border-crisis-border bg-crisis-card'}`}>
                    <div className="flex items-center justify-between">
                      <span className="text-xs text-crisis-text font-medium">{inc.type}</span>
                      <StatusBadge status={inc.severity_level} />
                    </div>
                    <p className="text-[9px] font-mono text-crisis-muted mt-0.5">{inc.location}</p>
                  </div>
                ))}
              </div>
            </div>

            <div className="bg-crisis-surface border border-crisis-border rounded-xl p-4">
              <h3 className="font-display text-[11px] tracking-widest text-crisis-text font-semibold mb-3">STAFF POSITIONS</h3>
              <div className="space-y-2">
                {staff.map(m => (
                  <div key={m.id} className="flex items-center justify-between">
                    <div className="flex items-center gap-2">
                      <div className={`w-6 h-6 rounded-full flex items-center justify-center text-[9px] font-bold
                        ${m.responding ? 'bg-crisis-red/20 text-crisis-red border border-crisis-red/40' : 'bg-crisis-cyan/10 text-crisis-cyan border border-crisis-cyan/30'}`}>
                        {m.avatar}
                      </div>
                      <div>
                        <p className="text-crisis-text text-[10px] font-medium">{m.name}</p>
                        <p className="text-crisis-muted text-[8px] font-mono">{m.zone}</p>
                      </div>
                    </div>
                    <span className={`text-[9px] font-mono ${m.responding ? 'text-crisis-red' : 'text-crisis-green'}`}>
                      {m.responding ? '● RESP' : '● ON'}
                    </span>
                  </div>
                ))}
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
  );
}
```

### `src/pages/VoiceAssistant.jsx`

```jsx
import { useState, useEffect } from 'react';
import { motion, AnimatePresence } from 'framer-motion';
import { Mic, MicOff, Volume2, Globe } from 'lucide-react';
import { useCrisis } from '../context/CrisisContext';

const LANGUAGES = ['English', 'हिन्दी', 'ಕನ್ನಡ', 'தமிழ்', 'বাংলা', 'Español', 'Français', '日本語', 'العربية'];

const DEMO_TRANSCRIPTS = [
  { lang: 'English', text: 'There is fire in the kitchen basement!',  ai: 'FIRE DETECTED — B1 Kitchen. Severity: Critical. Alerting Fire Response Team Alpha and notifying guests on B1–L3.' },
  { lang: 'हिन्दी',   text: 'कमरे 512 में कोई बेहोश हो गया है',        ai: 'MEDICAL EMERGENCY — Room 512, L5. Severity: High. Dispatching first-aid staff and calling 108 ambulance.' },
  { lang: 'ಕನ್ನಡ',   text: 'ಪೂಲ್ ಡೆಕ್‌ನಲ್ಲಿ ಒಬ್ಬರು ಬಿದ್ದಿದ್ದಾರೆ',        ai: 'FALL DETECTED — Pool Deck L5. Severity: High. Medical team dispatched. Area being cleared.' },
];

export function VoiceAssistant() {
  const { pushNotification } = useCrisis();
  const [listening, setListening]         = useState(false);
  const [transcript, setTranscript]       = useState('');
  const [aiResponse, setAiResponse]       = useState('');
  const [selectedLang, setSelectedLang]   = useState('English');
  const [processing, setProcessing]       = useState(false);
  const [waveform, setWaveform]           = useState(Array(20).fill(4));
  const [history, setHistory]             = useState([]);

  // Animate waveform when listening
  useEffect(() => {
    if (!listening) return;
    const interval = setInterval(() => {
      setWaveform(Array(20).fill(0).map(() => Math.random() * 32 + 4));
    }, 100);
    return () => clearInterval(interval);
  }, [listening]);

  const toggleListen = () => {
    if (listening) {
      setListening(false);
      setProcessing(true);
      const demo = DEMO_TRANSCRIPTS[Math.floor(Math.random() * DEMO_TRANSCRIPTS.length)];
      setTimeout(() => {
        setTranscript(demo.text);
        setProcessing(false);
        setTimeout(() => {
          setAiResponse(demo.ai);
          pushNotification('🎤 Voice report processed — AI classified incident', 'warning');
          setHistory(prev => [{ text: demo.text, response: demo.ai, time: new Date(), lang: demo.lang }, ...prev.slice(0, 4)]);
        }, 800);
      }, 1500);
    } else {
      setTranscript('');
      setAiResponse('');
      setListening(true);
    }
  };

  return (
    <div className="flex-1 overflow-y-auto bg-crisis-bg p-6">
      <div className="max-w-2xl mx-auto">
        <div className="flex items-center gap-3 mb-6">
          <Volume2 size={20} className="text-crisis-cyan" />
          <h1 className="font-display font-bold text-white text-lg tracking-widest">VOICE AI EMERGENCY ASSISTANT</h1>
        </div>

        {/* Language Selector */}
        <div className="mb-6">
          <p className="text-crisis-muted text-[10px] font-mono tracking-widest mb-2 flex items-center gap-1">
            <Globe size={11} /> SELECT LANGUAGE
          </p>
          <div className="flex flex-wrap gap-2">
            {LANGUAGES.map(lang => (
              <button
                key={lang}
                onClick={() => setSelectedLang(lang)}
                className={`px-3 py-1.5 rounded-full text-xs font-medium border transition-all
                  ${selectedLang === lang ? 'bg-crisis-cyan/20 border-crisis-cyan/50 text-crisis-cyan' : 'bg-crisis-card border-crisis-border text-crisis-muted hover:border-crisis-muted'}`}
              >
                {lang}
              </button>
            ))}
          </div>
        </div>

        {/* Voice Interface */}
        <div className="bg-crisis-surface border border-crisis-border rounded-2xl p-8 text-center">
          {/* Waveform */}
          <div className="flex items-center justify-center gap-1 h-16 mb-8">
            {waveform.map((h, i) => (
              <motion.div
                key={i}
                animate={{ height: h }}
                transition={{ duration: 0.05 }}
                className={`w-1.5 rounded-full transition-colors ${listening ? 'bg-crisis-red' : 'bg-crisis-muted/40'}`}
                style={{ minHeight: 4 }}
              />
            ))}
          </div>

          {/* Mic Button */}
          <button
            onClick={toggleListen}
            className={`
              relative w-24 h-24 rounded-full border-2 mx-auto flex items-center justify-center transition-all duration-300 mb-4
              ${listening
                ? 'bg-crisis-red border-crisis-red shadow-[0_0_40px_rgba(255,26,26,0.6)] animate-pulse-red'
                : 'bg-crisis-card border-crisis-border hover:border-crisis-cyan/50 hover:shadow-[0_0_20px_rgba(0,245,255,0.2)]'
              }
            `}
          >
            {listening ? <MicOff size={32} className="text-white" /> : <Mic size={32} className="text-crisis-cyan" />}
            {listening && <div className="absolute inset-0 rounded-full border-2 border-crisis-red/50 animate-ping" />}
          </button>

          <p className="font-display font-bold text-sm text-crisis-text tracking-widest mb-1">
            {processing ? 'PROCESSING…' : listening ? 'RECORDING — TAP TO STOP' : 'TAP TO REPORT EMERGENCY'}
          </p>
          <p className="text-crisis-muted text-xs font-mono">Language: {selectedLang} · AI-powered · Auto-translate</p>

          {/* Processing indicator */}
          {processing && (
            <div className="mt-4 flex items-center justify-center gap-2">
              <div className="w-4 h-4 border-2 border-crisis-cyan border-t-transparent rounded-full animate-spin" />
              <span className="text-crisis-cyan text-xs font-mono">AI classifying incident…</span>
            </div>
          )}
        </div>

        {/* Transcript + AI Response */}
        <AnimatePresence>
          {transcript && (
            <motion.div
              initial={{ opacity: 0, y: 20 }}
              animate={{ opacity: 1, y: 0 }}
              className="mt-4 space-y-3"
            >
              <div className="bg-crisis-surface border border-crisis-border rounded-xl p-4">
                <p className="text-crisis-muted text-[10px] font-mono tracking-widest mb-1">TRANSCRIPT</p>
                <p className="text-crisis-text text-sm">"{transcript}"</p>
              </div>
              {aiResponse && (
                <div className="bg-crisis-red/10 border border-crisis-red/40 rounded-xl p-4">
                  <p className="text-crisis-red text-[10px] font-mono tracking-widest mb-1">AI CLASSIFICATION & ACTION</p>
                  <p className="text-crisis-text text-sm">{aiResponse}</p>
                </div>
              )}
            </motion.div>
          )}
        </AnimatePresence>

        {/* History */}
        {history.length > 0 && (
          <div className="mt-6">
            <p className="text-crisis-muted text-[10px] font-mono tracking-widest mb-3">RECENT VOICE REPORTS</p>
            <div className="space-y-2">
              {history.map((h, i) => (
                <div key={i} className="bg-crisis-surface border border-crisis-border rounded-lg p-3">
                  <div className="flex items-center justify-between mb-1">
                    <span className="text-[9px] font-mono text-crisis-cyan">{h.lang}</span>
                    <span className="text-[9px] font-mono text-crisis-muted">{h.time.toLocaleTimeString()}</span>
                  </div>
                  <p className="text-crisis-text text-xs">"{h.text}"</p>
                  <p className="text-crisis-muted text-[10px] mt-1">→ {h.response}</p>
                </div>
              ))}
            </div>
          </div>
        )}
      </div>
    </div>
  );
}
```

### `src/pages/Reports.jsx`

```jsx
import { useCrisis } from '../context/CrisisContext';
import { BarChart, Bar, XAxis, YAxis, CartesianGrid, Tooltip, ResponsiveContainer, PieChart, Pie, Cell, LineChart, Line } from 'recharts';
import { FileBarChart, Download } from 'lucide-react';

const COLORS = ['#FF1A1A', '#FF6B1A', '#FFD700', '#00FF88', '#00F5FF'];

export function Reports() {
  const { incidents } = useCrisis();

  const byType = Object.entries(
    incidents.reduce((acc, i) => { acc[i.type] = (acc[i.type] || 0) + 1; return acc; }, {})
  ).map(([name, value]) => ({ name, value }));

  const bySeverity = ['Critical', 'High', 'Medium', 'Low'].map(s => ({
    name: s,
    count: incidents.filter(i => i.severity_level === s).length,
  }));

  const responseTime = [
    { time: '00:00', incidents: 0 },
    { time: '04:00', incidents: 1 },
    { time: '08:00', incidents: 3 },
    { time: '12:00', incidents: 5 },
    { time: '16:00', incidents: 2 },
    { time: '20:00', incidents: 4 },
    { time: '23:59', incidents: 1 },
  ];

  const CUSTOM_TOOLTIP = ({ active, payload, label }) => {
    if (!active || !payload?.length) return null;
    return (
      <div className="bg-crisis-surface border border-crisis-border rounded-lg p-3 text-xs font-mono">
        <p className="text-crisis-cyan mb-1">{label}</p>
        {payload.map((p, i) => (
          <p key={i} style={{ color: p.color }}>{p.name}: {p.value}</p>
        ))}
      </div>
    );
  };

  const stats = [
    { label: 'Total Incidents',    value: incidents.length,                                                   color: 'text-crisis-text'   },
    { label: 'Critical',           value: incidents.filter(i => i.severity_level === 'Critical').length,      color: 'text-crisis-red'    },
    { label: 'Resolved',           value: incidents.filter(i => i.status === 'Resolved').length,              color: 'text-crisis-green'  },
    { label: 'Avg Evac Progress',  value: `${Math.round(incidents.reduce((a, i) => a + i.evacuation_progress, 0) / incidents.length)}%`, color: 'text-crisis-yellow' },
    { label: 'Guests Affected',    value: incidents.reduce((a, i) => a + i.guest_count_affected, 0),          color: 'text-crisis-orange' },
    { label: 'Staff Responding',   value: 4,                                                                   color: 'text-crisis-cyan'   },
  ];

  return (
    <div className="flex-1 overflow-y-auto bg-crisis-bg p-6">
      <div className="max-w-5xl mx-auto">
        <div className="flex items-center justify-between mb-6">
          <div className="flex items-center gap-3">
            <FileBarChart size={20} className="text-crisis-cyan" />
            <h1 className="font-display font-bold text-white text-lg tracking-widest">INCIDENT ANALYTICS & REPORTS</h1>
          </div>
          <button className="flex items-center gap-2 px-4 py-2 rounded border border-crisis-cyan/40 bg-crisis-cyan/10 text-crisis-cyan text-xs font-mono hover:bg-crisis-cyan/20">
            <Download size={13} />
            EXPORT PDF REPORT
          </button>
        </div>

        {/* Stat Cards */}
        <div className="grid grid-cols-6 gap-3 mb-6">
          {stats.map(stat => (
            <div key={stat.label} className="bg-crisis-surface border border-crisis-border rounded-xl p-4 text-center">
              <p className={`text-2xl font-display font-black ${stat.color}`}>{stat.value}</p>
              <p className="text-crisis-muted text-[9px] font-mono mt-1 leading-tight">{stat.label}</p>
            </div>
          ))}
        </div>

        <div className="grid grid-cols-2 gap-4 mb-4">
          {/* Incidents by Type */}
          <div className="bg-crisis-surface border border-crisis-border rounded-xl p-5">
            <h3 className="font-display text-[11px] tracking-widest text-crisis-text font-semibold mb-4">INCIDENTS BY TYPE</h3>
            <ResponsiveContainer width="100%" height={200}>
              <BarChart data={byType} margin={{ top: 0, right: 0, left: -20, bottom: 0 }}>
                <CartesianGrid strokeDasharray="3 3" stroke="#1A2E4A" />
                <XAxis dataKey="name" tick={{ fill: '#2A3F5F', fontSize: 8, fontFamily: 'monospace' }} />
                <YAxis tick={{ fill: '#2A3F5F', fontSize: 9, fontFamily: 'monospace' }} />
                <Tooltip content={<CUSTOM_TOOLTIP />} />
                <Bar dataKey="value" radius={[4, 4, 0, 0]}>
                  {byType.map((_, i) => <Cell key={i} fill={COLORS[i % COLORS.length]} />)}
                </Bar>
              </BarChart>
            </ResponsiveContainer>
          </div>

          {/* Incidents by Severity */}
          <div className="bg-crisis-surface border border-crisis-border rounded-xl p-5">
            <h3 className="font-display text-[11px] tracking-widest text-crisis-text font-semibold mb-4">BY SEVERITY</h3>
            <ResponsiveContainer width="100%" height={200}>
              <PieChart>
                <Pie data={bySeverity} dataKey="count" nameKey="name" cx="50%" cy="50%" outerRadius={80} label={({ name, percent }) => `${name} ${(percent * 100).toFixed(0)}%`} labelLine={false}>
                  {bySeverity.map((_, i) => <Cell key={i} fill={COLORS[i]} />)}
                </Pie>
                <Tooltip content={<CUSTOM_TOOLTIP />} />
              </PieChart>
            </ResponsiveContainer>
          </div>
        </div>

        {/* Timeline */}
        <div className="bg-crisis-surface border border-crisis-border rounded-xl p-5">
          <h3 className="font-display text-[11px] tracking-widest text-crisis-text font-semibold mb-4">INCIDENT TIMELINE (TODAY)</h3>
          <ResponsiveContainer width="100%" height={150}>
            <LineChart data={responseTime} margin={{ top: 0, right: 10, left: -20, bottom: 0 }}>
              <CartesianGrid strokeDasharray="3 3" stroke="#1A2E4A" />
              <XAxis dataKey="time" tick={{ fill: '#2A3F5F', fontSize: 9, fontFamily: 'monospace' }} />
              <YAxis tick={{ fill: '#2A3F5F', fontSize: 9, fontFamily: 'monospace' }} />
              <Tooltip content={<CUSTOM_TOOLTIP />} />
              <Line type="monotone" dataKey="incidents" stroke="#00F5FF" strokeWidth={2} dot={{ fill: '#00F5FF', r: 4 }} activeDot={{ r: 6, fill: '#FF1A1A' }} />
            </LineChart>
          </ResponsiveContainer>
        </div>
      </div>
    </div>
  );
}
```

---

## 9. Root Files

### `src/App.jsx`

```jsx
import { Routes, Route, Navigate } from 'react-router-dom';
import { CrisisProvider } from './context/CrisisContext';
import { Header }        from './components/layout/Header';
import { Login }         from './pages/Login';
import { Dashboard }     from './pages/Dashboard';
import { IncidentLog }   from './pages/IncidentLog';
import { DigitalTwin }   from './pages/DigitalTwin';
import { VoiceAssistant } from './pages/VoiceAssistant';
import { Reports }       from './pages/Reports';
import { useState }      from 'react';

function ProtectedLayout({ user, children }) {
  return (
    <CrisisProvider>
      <div className="flex flex-col h-screen overflow-hidden crt-overlay">
        <Header user={user} />
        <div className="flex flex-1 overflow-hidden">
          {children}
        </div>
      </div>
    </CrisisProvider>
  );
}

export default function App() {
  const [user, setUser] = useState(null);

  const handleLogin = (userData) => setUser(userData);
  const handleLogout = () => setUser(null);

  if (!user) {
    return (
      <Routes>
        <Route path="*" element={<Login onLogin={handleLogin} />} />
      </Routes>
    );
  }

  return (
    <ProtectedLayout user={user}>
      <Routes>
        <Route path="/"             element={<Navigate to="/dashboard" replace />} />
        <Route path="/dashboard"    element={<Dashboard />} />
        <Route path="/incidents"    element={<IncidentLog />} />
        <Route path="/digital-twin" element={<DigitalTwin />} />
        <Route path="/voice"        element={<VoiceAssistant />} />
        <Route path="/reports"      element={<Reports />} />
        <Route path="*"             element={<Navigate to="/dashboard" replace />} />
      </Routes>
    </ProtectedLayout>
  );
}
```

### `src/main.jsx`

```jsx
import React from 'react'
import ReactDOM from 'react-dom/client'
import { BrowserRouter } from 'react-router-dom'
import App from './App.jsx'
import './index.css'

ReactDOM.createRoot(document.getElementById('root')).render(
  <React.StrictMode>
    <BrowserRouter>
      <App />
    </BrowserRouter>
  </React.StrictMode>,
)
```

### `index.html`

```html
<!doctype html>
<html lang="en" class="dark">
  <head>
    <meta charset="UTF-8" />
    <link rel="icon" type="image/svg+xml" href="/vite.svg" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>CrisisSync AI — Emergency Response Platform</title>
    <meta name="description" content="Rapid Crisis Response for Hospitality" />
    <link rel="preconnect" href="https://fonts.googleapis.com">
    <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
    <link href="https://fonts.googleapis.com/css2?family=Orbitron:wght@400;600;700;900&family=Exo+2:wght@300;400;500;600&family=JetBrains+Mono:wght@400;500&display=swap" rel="stylesheet">
  </head>
  <body>
    <div id="root"></div>
    <script type="module" src="/src/main.jsx"></script>
  </body>
</html>
```

### `postcss.config.js`

```js
export default {
  plugins: {
    tailwindcss: {},
    autoprefixer: {},
  },
}
```

---

## 10. Cursor Studio Quick Start

Open terminal in Cursor Studio and run:

```bash
# 1. Create Vite project
npm create vite@latest crisisync-ai -- --template react
cd crisisync-ai

# 2. Install all dependencies
npm install react-router-dom framer-motion lucide-react recharts clsx date-fns
npm install -D tailwindcss postcss autoprefixer
npx tailwindcss init -p

# 3. Replace all config files with the ones above
# Paste each file into its corresponding path

# 4. Run the dev server
npm run dev
```

**Cursor Studio AI Prompt** (paste into Cursor chat for instant scaffold):

```
Create the CrisisSync AI project structure as described. Files to create:
1. tailwind.config.js (with crisis color tokens + custom keyframes)
2. src/index.css (with Google Fonts import + custom utility classes)
3. src/data/incidents.js, sensors.js, staff.js, mapData.js
4. src/context/CrisisContext.jsx
5. src/components/ui/*.jsx (PulsingDot, StatusBadge, SOSButton, AnimatedCounter)
6. src/components/layout/*.jsx (Header, Sidebar, RightPanel)
7. src/components/dashboard/*.jsx (IncidentCard, PropertyMap, EvacuationProgress, AlertsBroadcast)
8. src/components/modals/*.jsx (BroadcastModal, EscalateModal)
9. src/pages/*.jsx (Login, Dashboard, IncidentLog, DigitalTwin, VoiceAssistant, Reports)
10. src/App.jsx and src/main.jsx
```

---

## 11. Feature–Component Matrix

| Feature                          | Component(s)                          |
|----------------------------------|---------------------------------------|
| Login (multi-role)               | `Login.jsx`                           |
| Live incident feed               | `Dashboard.jsx`, `IncidentCard.jsx`   |
| Sensor sidebar                   | `Sidebar.jsx`                         |
| Interactive property map         | `PropertyMap.jsx`, `DigitalTwin.jsx`  |
| Broadcast SMS / PA               | `BroadcastModal.jsx`                  |
| Escalate to 911 / 100 / 108      | `EscalateModal.jsx`                   |
| SOS one-tap button               | `SOSButton.jsx`                       |
| Evacuation progress              | `EvacuationProgress.jsx`              |
| Digital Twin (live floor view)   | `DigitalTwin.jsx`                     |
| Voice + multilingual assistant   | `VoiceAssistant.jsx`                  |
| Incident log + CSV export        | `IncidentLog.jsx`                     |
| Analytics + charts               | `Reports.jsx`                         |
| Real-time toast notifications    | `Dashboard.jsx` (AnimatePresence)     |
| Staff position tracker           | `Sidebar.jsx`, `DigitalTwin.jsx`      |
| AI suggested actions             | `IncidentCard.jsx` (ai_suggested_action field) |
| Alarm flash overlay              | `Dashboard.jsx`                       |
| API payload display              | `IncidentCard.jsx` (expanded view)    |

---

## 12. AI Models Used in This Frontend

| Purpose                              | Model / Technology                                                    |
|--------------------------------------|-----------------------------------------------------------------------|
| **Incident Classification**          | `GPT-4o` / `Claude 3.5 Sonnet` — classifies sensor data into structured incident types and severity levels |
| **AI Suggested Actions**             | `Claude 3.5 Sonnet` (Anthropic) — generates context-aware response recommendations per incident |
| **Voice Transcription**              | `OpenAI Whisper v3` — multilingual speech-to-text at the edge         |
| **Voice Intent Classification**      | `Gemini 1.5 Flash` — fast intent parsing for real-time voice emergency reports |
| **Multilingual Translation**         | `Helsinki-NLP/opus-mt` (HuggingFace) — translates non-English voice reports to structured English payloads |
| **Camera / Fall Detection**          | `YOLOv8-Pose` (Ultralytics) — real-time computer vision for fall/anomaly detection on RTSP feeds |
| **Facial Recognition (Access)**      | `InsightFace ArcFace` — unauthorized person detection at access control points |
| **Sensor Anomaly Detection**         | `Isolation Forest` (scikit-learn) / `LSTM Autoencoder` — detects deviations in smoke, temperature, vibration streams |
| **Evacuation Route Optimization**    | `Dijkstra + A* pathfinding` — dynamically recalculates safe exit routes based on blocked zone data |
| **Post-Incident Report Generation**  | `Claude 3 Haiku` — auto-generates concise post-incident PDF summaries from logged event data |
| **NLP Broadcast Drafting**           | `GPT-4o-mini` — generates broadcast message drafts from incident metadata |
| **Sentiment & Panic Detection**      | `RoBERTa` fine-tuned on emergency comms — detects panic language in guest-submitted text reports |

---

> **Note**: All AI responses shown in the frontend (sensor alerts, `ai_suggested_action` fields, voice classification outputs) are simulated with static mock data. Connect the API endpoints in `CrisisContext.jsx` to wire up your live FastAPI + AI backend.
