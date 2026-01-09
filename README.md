# 🔐 Premium Password Strength Checker

A modern **Python GUI application** that checks password strength in real time and provides visual feedback and improvement suggestions.  
Built using **CustomTkinter**, this project focuses on usability, security rules, and clean UI design.

---

## 🚀 Features

- Real-time password strength analysis
- Animated progress bar with smooth transitions
- Color-coded strength levels:
  - 🔴 Weak
  - 🟠 Medium
  - 🟢 Strong
- Smart suggestions to improve weak passwords
- Show / Hide password toggle
- Detects common passwords and repeating characters
- Modern dark-themed UI
- Multithreading for smooth UI performance

---

## 🧠 Password Evaluation Logic

The password strength is evaluated based on:
- Length (minimum 8–12 characters recommended)
- Uppercase letters (A–Z)
- Lowercase letters (a–z)
- Numbers (0–9)
- Special characters (!@#$%^&* etc.)
- Avoidance of common passwords
- Avoidance of repeated characters and numeric-only passwords

Each rule contributes to a strength score, which is then mapped to a visual indicator.

---

## 🛠️ Tech Stack

- **Language:** Python
- **GUI Framework:** CustomTkinter
- **Libraries Used:**
  - `customtkinter`
  - `re`
  - `threading`
  - `time`

---

