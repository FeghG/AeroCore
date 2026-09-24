# AeroCore Coding Standard (MISRA C++ Subset)

This document establishes the code quality and safety rules for the AeroCore flight computing and simulation system.

---

## 1. Scope
* **Core Systems (core/)**: High-performance flight physics, math, and data handling (C++17/C++must strictly adherere** to this standard.
* **Graphical Interface (hmi/)**: Qt 6 / QML code is excluded from strict MISRA compliance, as the HMI layer is non-flight-critical.

---

## 2. Rule CategoMandatorydatory** — Deviations are strictly prohibiRequiredquired** — Deviations are allowed only with a formal Deviation RecAdvisoryvisory** — Recommended best practices for code quality and maintainability.

---

## 3. Critical MISRA C++:2023 Rules for AeroCore

| Rule / Section | Description | Purpose in AeroCore |
| :--- | :--- | :11.6.211.6.2** | Disallow reading uninitialized objects | Ensures deterministic telemetry and physics computat7.0.5 / 7.0.6 7.0.6** | Restrict implicit type conversions | Prevents precision loss in 6DoF flight physics matri8.18.28.18.2** | Prohibit assignment inside conditions if (x = y) | Eliminates accidental assignments and logic bMemory PolicyPolNo dynamic memory allocation (heap)(heap)** post-init | Enforces Hard Real-Time zero-allocation ring buff15.0.1 / 15.1.315.1.3** | Enforce Rule of Zero for special member functions | Guarantees safe data frame and telemetry stream handlConcurrencyrrency** | Strict control over shared data and thread synchronization | Prevents race conditions between SITL generator and cExceptions/RTTIs/RTTI** | Restrict or disable C++ exceptions / RTTI | Guarantees deterministic execution time in RT loops |

---

## 4. Real-Time Error Handling (Data Core)
* Sensor errors or dropped network packets must never break the main loop.
* All errors are mapped into explicit frame status codes: OK, DEGRADED, CRITICAL.

---

## 5. Static Analysis & Compiler Flags
Compliance is automatically verified during bCompiler Flags Flags**: -Wall -Wextra -Werror -Wconversion -Wsign-conversion
* **CI Tools**: clang-tidy (with bugprone-*, cert-*, and cppcoreguidelines-* modules)
