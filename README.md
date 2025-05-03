# Pomodoro Timer Web App (Vue 3 + Vite)

A modern, minimal, and focused Pomodoro timer built using Vue 3, Vite, Bootstrap 5, and Supabase. This app allows users to set their study duration, track session history, and store data securely in a Supabase database.

---

## 📁 Project Structure

```
pomodoro-timer-vue/
├── public/
├── src/
│   ├── assets/
│   ├── components/
│   │   ├── PomodoroTimer.vue
│   │   ├── TimerControls.vue
│   │   └── Button.vue
│   ├── composables/
│   │   └── useSupabase.js
│   ├── router/
│   │   └── index.js
│   ├── views/
│   │   ├── HomeView.vue
│   │   └── HistoryView.vue
│   ├── App.vue
│   ├── main.js
│   └── styles/
│       └── (optional custom css)
├── index.html
├── .gitignore
├── package.json
├── postcss.config.js
├── tailwind.config.js (if used)
└── vite.config.js
```

---

## ⚙️ Technologies Used

| Layer       | Tools / Frameworks             |
|-------------|---------------------------------|
| Frontend    | Vue 3, Vite, Bootstrap 5       |
| State Mgmt  | Composition API                |
| Database    | Supabase (PostgreSQL backend)  |
| Deployment  | (Not Specified)                |

---

## 🔌 Supabase API Usage

All session history and durations are stored and fetched using Supabase. Interactions include:
- `insert()` a new Pomodoro session on completion
- `select()` history ordered by `created_at`

Example:
```js
const { data, error } = await supabase
  .from('study_sessions')
  .select('*')
  .order('created_at', { ascending: false })
```

---

## 🧠 Features

- ⏱ Input custom Pomodoro duration (minutes)
- ✅ Start / Pause / Reset controls
- 📚 Study history dashboard
- 📦 Supabase integration for persistent session logging
- 🎨 Clean, modern UI inspired by calm Japanese design aesthetics

---

## 📊 System Flowchart

### 🔹 Frontend Flow

```
User
 └─▶ HomeView.vue
       ├─▶ PomodoroTimer.vue
       ├─▶ TimerControls.vue
       └─▶ Button.vue (navigates to History)

 └─▶ HistoryView.vue
       └─▶ StudyHistory.vue (renders session list)
```

### 🔸 Backend Flow (via Supabase API)

```
PomodoroTimer.vue
 ├─▶ saveSession() ──▶ Supabase API ──▶ INSERT into 'study_sessions'

StudyHistory.vue
 ├─▶ onMounted() ──▶ Supabase API ──▶ SELECT * from 'study_sessions'
```

---

## 🗃️ Database Schema: `study_sessions`

| Column        | Type      | Constraints            |
|---------------|-----------|------------------------|
| id            | UUID      | Primary Key, auto-gen  |
| duration_min  | Integer   | Not null               |
| created_at    | Timestamp | Default: now()         |
| note          | Text      | Optional               |

---

## 🧭 Navigation

| Page         | Route        | Description                       |
|--------------|--------------|-----------------------------------|
| Home         | `/`          | Main Pomodoro timer UI            |
| History      | `/history`   | Study session log                 |

---

## 📝 Author & License

This project is maintained by the creator. All rights reserved.

License: MIT