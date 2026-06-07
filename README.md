# Angelos Tsanaktsidis

**Systems & Security Engineer** — low-level C/C++ on Linux, embedded/RTOS, post-quantum cryptography, secure transport, and kernel-bypass networking, with peer-reviewed research behind the work.

Endpoint / Linux / Cloud security · Linux kernel, eBPF/XDP, DPDK · containers · ARM TrustZone-M / TF-M · TLS 1.3 & hybrid PQC · QEMU multi-ISA profiling · performance debugging to root cause.

📍 EU (Greek) citizen · open to relocation · [LinkedIn](https://www.linkedin.com/in/a-tsanak) · angelostsanak@gmail.com

---

## ⚠️ Read this first — what is public here, and what is not

These public repositories are **review / demo versions**, published so an engineer can read real code, build it, and check results against a methodology. They are **representative implementations** and **sanitized artifacts** — the core ideas are demonstrated publicly, but the **complete production and research codebases are private** due to NDA, EU-consortium (Horizon FOCAL), startup, and academic-publication constraints.

Concretely, that means:

- **No invented evidence.** Every number quoted inside a repo comes from result artifacts checked into that repo. Where a CV headline figure was produced by the larger private campaign, I say so and do **not** restate it as a public result.
- **Public artifacts are a subset.** For example, the kernel-bypass repo's *public* validated CSV tops out around ~1.19 Gbps on a small lab, whereas the full private campaign reached the higher figure quoted on my CV; the embedded-PQC repo's *public* CSV shows a 166.6× HQC/ML-KEM cycle ratio rather than the cross-device median on my CV. The public repos demonstrate the **method and the engineering**, not the full dataset.
- **What's excluded:** raw result archives, paper drafts/LaTeX, private datasets and trained weights, device credentials, and internal reports. Each repo lists exactly what was held back.

If you are reviewing me after seeing my CV, the section below maps each CV claim to the repo where you can inspect the underlying engineering yourself.

---

## 🧭 Reviewer guide — how to evaluate this in ~15 minutes

Every pinned repo follows the same contract so you can move fast:

1. **Top of the README** states *what the repo proves* and its *public-scope note*.
2. **Build / Run** gives exact commands and the expected console/output files.
3. **Results** point to a single *trusted* CSV/summary that is the only source of truth — generated artifacts and audits sit beside it.
4. **Limitations** state the evidence boundary plainly (e.g. QEMU vs. silicon, modelled vs. probed energy, lab-scale vs. full campaign).

Fastest path: open the repo, read *What this repo proves* → skim the *Results Summary* table → open the trusted CSV. You do not need to build anything to judge the methodology.

---

## 📌 Pinned repositories — what each one proves

| Repo | What it demonstrates publicly | Public-verifiable evidence | Held private |
|---|---|---|---|
| **[zephyr-pqc-benchmarking](https://github.com/atsanak/zephyr-pqc-benchmarking)** | Cross-ISA embedded PQC measurement in C on Zephyr/QEMU: KEM/signature ops isolated per operation, multi-metric harness (cycles, tail percentiles, stack/heap, entropy, modelled energy). | `results/final/validated_results.csv` — 498 validated rows, 15 PQC parameter sets, 13 ISA labels / QEMU targets, 1000 iters/row; 166.6× median HQC/ML-KEM cycle ratio. | Full cross-device dataset, energy-probe runs, paper artifacts. |
| **[kernel-bypass-pqc-benchmarking](https://github.com/atsanak/kernel-bypass-pqc-benchmarking)** | PQC-authenticated handshake + AES-256-GCM data plane over Linux, AF_PACKET, **eBPF/XDP (AF_XDP)**, **DPDK**, F-Stack, mTCP, Seastar — same protocol across stacks for an apples-to-apples transport comparison. | `results/final/validated_results.csv` — 55 validated rows across 7 transports; e.g. Seastar 1187 Mbps, F-Stack handshake 2.03 ms vs 4.77 ms kernel TCP. Every raw artifact hashed. | High-rate (multi-Gbps) campaign, full backend matrix runs, NIC-lab captures. |
| **[hybrid-pqc-tls-uav](https://github.com/atsanak/hybrid-pqc-tls-uav)** | Hybrid PQ key exchange over TLS 1.3 for UAV telemetry: ECDH P-256 **+ ML-KEM** for session keys, ECDSA P-256 **+ ML-DSA** per-chunk auth, AES-256-GCM payloads with end-to-end SHA-256 verification, on Jetson Orin. | Correctness gates (shared-secret match, 0 sig/decrypt failures, matching SHA-256) + WiFi throughput campaign (≈22.3 MB/s at 96 KiB chunks). | 85-pair algorithm sweep, full power/RTT telemetry, hardware campaign data. |
| **[pqc-edge-ai-co-optimization](https://github.com/atsanak/pqc-edge-ai-co-optimization)** | Edge→cloud split inference (AttentionGrid tile selection) under classical vs. PQC hybrid transport, measuring the data/accuracy/latency trade-off. | `results/verified_summary.csv` — 340 rows; AttentionGrid cuts on-wire upload ~76% (341→83 MB) while holding detection quality; PQC vs classical deltas included. | Full datasets/weights, server-GPU energy-per-frame campaign, raw run dirs. |
| **[zephyr-embedded-pqc-benchmarking](https://github.com/atsanak/zephyr-embedded-pqc-benchmarking)** | Zephyr module wiring `mlkem-native`/`mldsa-native` with **ACVP/KAT validation**, timing-smoke (CT) markers, and a "cost-of-assurance" benchmark of PQC primitives + protocol paths. | Paired PQCP-vs-baseline primitive CSVs on `qemu_x86_64` + build-only footprint rows for `nucleo_h743zi`/`mps2-an385`, each hashed in a manifest. | TrustZone-M/TF-M secure-world enclave measurements, board-run timing. |

---

## 🔗 CV → repository mapping

For a reviewer holding my CV (Software Engineer / Security Engineer / Endpoint-Linux-Cloud Security variants):

| CV claim | Where to inspect the engineering | Honest scope note |
|---|---|---|
| "Cross-architecture PQC benchmarking framework in C across 13 ISAs and a 49-metric suite" | [zephyr-pqc-benchmarking](https://github.com/atsanak/zephyr-pqc-benchmarking) | Public CSV covers 13 ISA labels and a multi-metric set on QEMU; the 135× median speedup figure is from the full private cross-device campaign, not the public subset. |
| "Kernel-bypass data paths with eBPF/XDP and DPDK; 79% latency cut, p99 48.6 µs, 9.49 Gbps" | [kernel-bypass-pqc-benchmarking](https://github.com/atsanak/kernel-bypass-pqc-benchmarking) | Public repo shows the protocol, all transport backends as source, and a lab-scale validated CSV. The multi-Gbps / µs-tail headline figures are from the full private campaign. |
| "Hybrid post-quantum TLS 1.3 on NVIDIA Jetson; dual-signature path isolated as ~4× AES-GCM across an 85-pair sweep" | [hybrid-pqc-tls-uav](https://github.com/atsanak/hybrid-pqc-tls-uav) | Public repo proves the hybrid protocol + correctness + a throughput campaign; the 85-pair sweep and power telemetry are private. |
| "Adaptive edge-to-cloud perception pipeline; 76% less on-wire data, 2.91× throughput, 4.4× less GPU energy/frame" | [pqc-edge-ai-co-optimization](https://github.com/atsanak/pqc-edge-ai-co-optimization) | The ~76% upload reduction is verifiable in the public CSV; the throughput/energy multipliers come from the fuller private campaign. |
| "ARM TrustZone-M / TF-M trusted-execution layer; secure-world overhead ~2% avg (5.5% worst)" | [zephyr-embedded-pqc-benchmarking](https://github.com/atsanak/zephyr-embedded-pqc-benchmarking) | Public repo shows the validation harness (ACVP/KAT) and a QEMU "cost-of-assurance" methodology; the TrustZone-M/TF-M secure-world numbers themselves are private. |
| "Microarchitecture simulators (C++): pipelined MIPS32 + configurable cache" | Not yet public | Coursework artifact; can be shared on request. |

---

## 🛠️ Core stack with public evidence

**Languages:** C, C++ (modern C++), Python, Bash · **Embedded/RTOS:** Zephyr, FreeRTOS, QEMU multi-ISA, west, CMake/Ninja · **Linux systems:** eBPF/XDP, DPDK, AF_PACKET, perf, GDB/JTAG · **Security/crypto:** ML-KEM, ML-DSA, SLH-DSA, Falcon, HQC, Classic McEliece, AES-GCM, TLS 1.3 / hybrid PQC, ACVP/KAT, ARM TrustZone-M / TF-M · **Containers/automation:** Docker, CI-style reproducible pipelines.

## 🎓 Research & recognition

Accepted at **ACM SenSys** (embedded post-quantum key establishment); further work under review (ACM TACO, IFIP/IEEE VLSI-SoC, IEEE GLOBECOM, Springer chapter) on hybrid TLS, kernel-bypass PQC networking, and secure edge AI. **ISPASS 2026 Artifact Reviewer.** Because several of these are under review or embargo, the matching repositories are deliberately sanitized — the public code shows the engineering, not the unpublished results.

---

*Honesty note: I would rather show you a smaller, true, reproducible artifact than a polished claim you can't check. If a repo's public scope blocks something you need to evaluate, ask — I can often walk through the private system live under appropriate terms.*
