# Mood Reactive Code Editor

An experimental **VS Code extension** that adapts the coding environment to the developer’s psychological state in real time.

The system uses **computer vision (MediaPipe FaceMesh)** to estimate stress signals from the webcam and dynamically adjusts:

* 🎨 editor themes
* 🎧 ambient audio
* 💡 productivity suggestions

to better match the developer’s cognitive state while coding.

The project explores how **adaptive IDE environments** can improve focus, reduce stress, and enhance developer productivity.

---

# Features

### Real-Time Mood Detection

Uses **MediaPipe FaceMesh** to estimate facial signals such as:

* eye aspect ratio (blink/stress proxy)
* eyebrow tension
* mouth/jaw tension

These signals are combined into a **stress score (0–100)**.

---

### Adaptive Coding Environment

The extension modifies the IDE depending on the detected mood:

| Mood        | IDE Behavior                                                 |
| ----------- | ------------------------------------------------------------ |
| 😌 Calm     | Suggest deeper refactors and architectural improvements      |
| ⚡ Focused   | Encourage momentum with small refactors and helpers          |
| 🔥 Stressed | Suggest micro-steps, smaller tasks, and debugging strategies |

---

### Dynamic Theme Switching

The extension can automatically change the editor theme based on mood state.

Example:

```
calm → light theme  
focused → dark coding theme  
stressed → high contrast / minimal distraction
```

---

### Ambient Audio

Optional ambient background audio:

```
calm → calm.mp3
focused → focused.mp3
stressed → stressed.mp3
```

Tracks smoothly **fade between states**.

---

### Productivity Suggestions

A built-in suggestion engine provides contextual coding tips:

Examples:

**Stressed**

* break task into micro-steps
* run tests before editing
* reduce scope

**Focused**

* extract helper function
* write small refactor
* add type hints

**Calm**

* perform larger refactor
* extract module
* improve architecture

Suggestions appear in:

* status bar tooltip
* optional notifications

---

# Architecture

```
Webcam
   ↓
MediaPipe FaceMesh
   ↓
FastAPI Inference Service
   ↓
VSCode Extension (TypeScript)
   ↓
Mood Engine
   ↓
IDE Adaptation
(theme + audio + suggestions)
```

---

# Project Structure

```
mood-reactive-editor
│
├─ python/                 FastAPI stress inference service
│   ├─ main.py
│   └─ inference.py
│
├─ src/                    VSCode extension (TypeScript)
│   ├─ extension.ts
│   ├─ moodEngine.ts
│   ├─ audioPlayer.ts
│   └─ suggestionProvider.ts
│
├─ media/
│   └─ audio/
│
└─ package.json
```

---

# Installation

## 1 Install dependencies

```
npm install
npm run compile
```

---

## 2 Start the Python service

```
cd python

python -m venv .venv
source .venv/bin/activate

pip install -r requirements.txt

uvicorn main:app --host 127.0.0.1 --port 8765
```

---

## 3 Run the extension

Open the project in VS Code and press:

```
F5
```

A new **Extension Development Host** window will open.

---

# Usage

Enable monitoring:

```
Command Palette → Mood Editor: Toggle Monitoring
```

Optional:

```
POST /camera/start
```

The extension will begin adapting the environment based on detected mood.

---

# Privacy

This project is **privacy-first**.

* Webcam frames are **never stored**
* No data leaves the local machine
* Only **3 numeric signals per frame** are used internally

---

# Future Ideas

Possible improvements:

* smartwatch integration (heart rate / HRV)
* machine-learning stress models
* collaborative mood analytics
* IDE productivity research experiments

---

# License

MIT License
