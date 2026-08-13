# Astrex VPN Ecosystem

A modern, high-performance, cross-platform VPN ecosystem built from scratch with a focus on custom architecture, clean design, and speed. 

---

## 🏗️ Architecture & How It Works

Astrex operates on a **Hub-and-Node** distributed model:
* **The Central Hub (Rust / Axum):** Manages user data, traffic tracking, promo codes, and device authentication. It serves as the central brain.
* **The Server Nodes (Xray & Hysteria 2):** Individual server nodes connect back to the Hub via **WebSockets** to sync configuration and route client traffic dynamically. 

---

## 📱 Tech Stack & Components

| Component | Technology | Description |
| :--- | :--- | :--- |
| **Client App** | Kotlin Multiplatform (KMP), `sing-box` | Unified cross-platform client for Android, iOS, and macOS. |
| **Backend (Hub)** | Rust, Axum, WebSockets | High-performance async backend handling routing and APIs. |
| **Nodes** | Xray-core, Hysteria 2 | Anti-censorship core protocols with zero-restart hot-reloading. |

---

## 🔗 Ecosystem Repositories

* [Cross-Platform Client](https://github.com/theorynow/AstrexVPN-client) — KMP application code.
* [Landing & Site](https://github.com/theorynow/AstrexVPN-site) — Web landing page and trial distribution.
* [Server Hub](https://github.com/theorynow/AstrexVPN-server-hub) — Core backend API & management.
* [Server Node](https://github.com/theorynow/AstrexVPN-server-node) — Edge routing nodes.

---

## 📊 Monitoring & Documentation

* **Landing Page:** [astrex.club](https://astrex.club)
* **API Documentation:** [hub.astrex.skyfly.hackclub.app/docs](https://hub.astrex.skyfly.hackclub.app/docs)
* **Public Grafana Dashboard:** [View Live Metrics](https://grafana.hub.astrex.skyfly.hackclub.app/public-dashboards/f396f592ce994d128f9b2a321030ad58)
