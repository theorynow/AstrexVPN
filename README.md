# What is this repository?

This is the main repository that contains links to modules - the repositories that contains the entire VPN infrastructure.

---

## Architecture & How It Works

Astrex operates on a **Hub-and-Node** distributed model:
1. The central backend (i called it hub) acts as the “brain” of the network. It handles user registration, device authentication, promo code activation, and bandwidth monitoring. It provides a rest api for mobile and desktop clients and maintains persistent WebSocket connections with all registered edge nodes (required to connect clients to the node and disconnect them if all traffic quota is used up). The hub also provides the client application with a WebSocket to monitor the current amount of traffic consumed (everything runs on Centrifugo on the client side; for communication between the hub and the node, everything runs on plain WebSocket with retries if necessary).
2. A daemon (rust service) runs on each node, which establishes a connection to the hub via WebSockets when the system boots up. When a user’s traffic changes, the amount of traffic used is transmitted to the hub (since the hub is responsible for tracking traffic). When a user registers on a node, the hub notifies the node via WebSocket that the user needs to be added to the configuration, and depending on the protocol (Xray-core or Hysteria 2), the user is added by the daemon either via gRPC or via the rest api.
3. The client application interacts with the rest api of the Hub to retrieve the user’s traffic quota, obtain a list of available servers (nodes) to connect, and register the user on a node. After a server is selected, the hub registers the user on the node and checking the user’s traffic quota; the app then passes the settings to the built-in sing-box engine, which manages the local TUN interface.

---

## Tech Stack

1. *[AstrexVPN-client](https://github.com/theorynow/AstrexVPN-client)* -
Kotlin Multiplatform (KMP), sing-box.

2. *[AstrexVPN-server-hub](https://github.com/theorynow/AstrexVPN-server-hub)* - Rust, Axum, WebSockets, PostgreSQL, Centrifugo, observability stack (otecol, grafana, tempo, loki).

3. *[AstrexVPN-server-node](https://github.com/theorynow/AstrexVPN-server-node)* - Rust, Xray-core, Hysteria 2, WebSockets, gRPC.

4. *[AstrexVPN-site](https://github.com/theorynow/AstrexVPN-site)* - Next.js (App Router), React, TypeScript, Tailwind CSS v4, shadcn/ui.

## Monitoring & Documentation

* **Landing Page:** [astrex.club](https://astrex.club)
* **API Documentation:** [hub.astrex.skyfly.hackclub.app/docs](https://hub.astrex.skyfly.hackclub.app/docs)
* **Public Grafana Dashboard:** [dasboard](https://grafana.hub.astrex.skyfly.hackclub.app/public-dashboards/f396f592ce994d128f9b2a321030ad58)
