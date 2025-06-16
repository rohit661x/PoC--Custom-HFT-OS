# PoC--Custom-HFT-OS

                [ EXCHANGE COLOCATION DATA CENTER ]
 ┌────────────────────────────────────────────────────────────────┐
 │                   ① Exchange Market Data                       │
 │                   ② Order Entry/Matching Engine                │
 └────────────────────────────────────────────────────────────────┘
                                │
                                ▼
                [ FIRM'S COLOCATED RACK (Server in Same DC) ]
 ┌────────────────────────────────────────────────────────────────┐
 │                                                                │
 │   [ Ultra-Low-Latency Switch ]                                 │
 │           │             │                                       │
 │           ▼             ▼                                       │
 │  [ NIC / Custom OS Server ] ⇄ [ NIC / FPGA Server ]            │
 │           │             │                                       │
 │           ▼             ▼                                       │
 │  [ Market Data RX ]   [ Order TX Path ]                        │
 │           │             │                                       │
 │     ↳ Strategy Engine (on CPU)                                 │
 │           │             │                                       │
 │    ↳ Order Routing Module                                      │
 │                                                                │
 └────────────────────────────────────────────────────────────────┘
                                │
                                ▼
                     [ INTERNAL NETWORK CONNECTION ]
                                │
 ┌────────────────────────────────────────────────────────────────┐
 │                     ③ Main Trading Office                      │
 │     - Monitoring Dashboards                                    │
 │     - Logging/Replay Engines                                   │
 │     - Internal Latency Metrics                                 │
 └────────────────────────────────────────────────────────────────┘
                                │
                                ▼
               [ ④ Long-Term Storage / Database / Analytics ]
 ┌────────────────────────────────────────────────────────────────┐
 │   - Trade & Market Replay DB (e.g., kdb+, ClickHouse, custom)  │
 │   - Post-trade Analytics (Python, Rust, etc.)                  │
 │   - Compliance & Risk Monitors                                 │
 └────────────────────────────────────────────────────────────────┘