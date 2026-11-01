# ⏱️ Clash of Clans Upgrade & Boost Calculator

A lightweight, zero-dependency, fully offline Progressive Web App (PWA) designed to calculate true completion times for upgrades in **Clash of Clans** when factoring in sequential boosts (Builder Potions, Builder Bites, and Research Potions).

---

## ⚡ The Problem

In *Clash of Clans*, the UI displays the total nominal upgrade time remaining rather than adjusting dynamically for active temporary speed boosts. 

* **Builder Potions** run at **10× speed** for 1 hour (saving 9 hours).
* **Builder Bites** run at **2× speed** for 1 hour (saving 1 hour)[cite: 1].
* **Research Potions** run at **24× speed** for 1 hour (saving 23 hours).
* **Interaction:** Builder Bites and Builder Potions **do not stack simultaneously**[cite: 1]; they run sequentially[cite: 1].

Calculating multi-boost chains manually is error-prone. This tool calculates the exact real-world check-in timestamp and triggers audible alerts.

---

## ✨ Features

- **Sequential Boost Engine:** Accurately steps through Builder Potions (10×) first, then Builder Bites (2×)[cite: 1], and falls back to standard speed (1×).
- **Research/Lab Boosts:** Supports dedicated 24× speed calculations for laboratory upgrades.
- **100% Offline Capability:** Runs locally in any modern browser without an active internet connection.
- **Synthesized Audio Alert:** Built-in Web Audio API alarm sound that works without external MP3 dependencies.
- **One-Tap Calendar/Alarm Sync:** Generates a lightweight `.ics` file per timer to schedule system-level audible alarms directly in Google Calendar or your native clock/calendar app.
- **State Persistence:** Preserves active countdowns across browser reloads via `localStorage`.

---

## 📐 Boost Calculation Logic

### 1. Builder Upgrades (Home Village)
$$\text{BP Capacity} = P \times 10\text{ hrs (game work)}$$
$$\text{Bite Capacity} = B \times 2\text{ hrs (game work)}$$

- **Phase 1 (Builder Potions):** If $T_{\text{rem}} \le \text{BP Capacity}$, $\text{Real Time} = \frac{T_{\text{rem}}}{10}$.
- **Phase 2 (Builder Bites):** If remaining time $T_{\text{rem2}} \le \text{Bite Capacity}$, $\text{Real Time} = P + \frac{T_{\text{rem2}}}{2}$.
- **Phase 3 (Standard Speed):** Any remaining hours after all boosts run at normal $1\times$ speed:
  $$\text{Real Time} = P + B + (T_{\text{rem2}} - \text{Bite Capacity})$$

### 2. Lab Upgrades
$$\text{Lab Capacity} = P \times 24\text{ hrs (game work)}$$

- If $T_{\text{rem}} \le \text{Lab Capacity}$, $\text{Real Time} = \frac{T_{\text{rem}}}{24}$.
- If $T_{\text{rem}} > \text{Lab Capacity}$, $\text{Real Time} = P + (T_{\text{rem}} - \text{Lab Capacity})$.

---

## 🚀 Installation & Setup

### Method 1: GitHub Pages (Recommended for Android PWA)
1. Fork or push this repository to GitHub.
2. Navigate to **Settings** → **Pages**.
3. Under **Branch**, select `main` (or `master`) and directory `/ (root)`, then click **Save**.
4. Visit your deployed URL (`https://<username>.github.io/<repo>/`) on Chrome or Brave on Android.
5. Tap the browser menu (⋮) → **Add to Home screen** / **Install app**.

### Method 2: Direct Local File (No Server Needed)
1. Download `index.html` directly to your phone's local storage (e.g., `/Downloads`).
2. Open Chrome/Brave and type:
   ```text
   file:///storage/emulated/0/Download/index.html
