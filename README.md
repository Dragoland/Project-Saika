# **Project Saika**

**Author:** [Dragoland](https://github.com/Dragoland)      
**Company:** SaikaNET Studio (Coming Soon)     
**Concept Date:** January, 2026     
**Document Status:** Planning     
**Core Philosophy:** *"Computers are believers, and users, their gods."*

---

## **Table of Contents**
1.  [Vision and Philosophy](#1-vision-and-philosophy)
2.  [General Project Architecture](#2-general-project-architecture)
3.  [Component: SaikaOS](#3-component-saikaos)
4.  [Component: SaikaDesktop Environment (SDE)](#4-component-saikadesktop-environment-sde)
5.  [Component: Saika Suite](#5-component-saika-suite)
6.  [Component: Saika Display Kiosk & Orchestrator (SDKO)](#6-component-saika-display-kiosk--orchestrator-sdko)
7.  [Technical Architecture and Tech Stack](#7-technical-architecture-and-tech-stack)
8.  [Development Roadmap](#8-development-roadmap)
9.  [Strategy, Community, and Sustainability](#9-strategy-community-and-sustainability)

---

## **1. Vision and Philosophy**

**Project Name:** Saika (Japanese: 彩華, "Colorful/Flourishing Flower").

**General Vision:** To create a comprehensive personal computing ecosystem, based on GNU/Linux, where the interface and system behavior are fluid, adaptive, and proactive. Saika aims to reduce the friction between user intent and machine action, offering a coherent and highly customizable experience across all its components.

**Philosophical Pillars:**
1.  **Contextual Adaptability (Context-Aware):** The system observes context (active applications, connected peripherals, time, power state) and suggests or automatically activates optimal behavioral profiles (desktop modes, notification rules, performance settings).
2.  **Deep Coherence:** From the kernel to the user interface, all parts must feel like members of a unified whole. User experience is prioritized over developer convenience in key design decisions.
3.  **Empowerment through Clarity:** Offer a high degree of customization and control, presented in an organized and accessible manner, avoiding overwhelming complexity. "Power to the user, not overload."
4.  **Elegant Efficiency:** Prioritize performance and low resource consumption, using modern technologies and efficient code, without sacrificing visual fluidity or responsiveness.
5.  **Integrated, Not Isolated Ecosystem:** Build exceptional native tools (*Saika Suite*) while seamlessly integrating and enhancing the best existing open-source software, fostering interoperability.

**Motto:** *"Flow with your work."*

---

## **2. General Project Architecture**

Project Saika is a meta-project encompassing several interconnected but independent sub-projects under the umbrella organization **SaikaNET Studio**. Its structure is modular:

```
Project Saika (SaikaNET Studio)
├── SaikaOS (The base distribution)
├── SaikaDesktop Environment - SDE (The adaptable graphical environment)
├── Saika Suite (The key native applications)
├── Saika Display Kiosk & Orchestrator - SDKO (Session & profile manager)
└── SaikaNET SDK & Tools (For external developers)
```

**Modularity Principle:** Components can be used independently. Example: SDE can be installed on vanilla Arch Linux; Saika Suite apps can run in other Qt environments.

---

## **3. Component: SaikaOS**

**Description:** A general-purpose, rolling-release GNU/Linux distribution aimed at users who value continuous updates, control, and a polished, integrated experience.

**Technical Base:**
*   **Foundation:** Based on **Arch Linux**. Uses official Arch repositories as the primary and trusted base for 95% of system and user software.
*   **Main Differentiation:** It is not a "fork." It is a **curation and integration layer**. SaikaOS adds:
    1.  **Own Repositories (`saika-core`, `saika-extra`):** Contain project-specific packages (SDE, Saika Suite, SDKO, custom kernels, themes, filtered non-free drivers).
    2.  **Opinionated Default Configuration:** A ready-to-use system with SDE, multimedia codecs, essential development tools, and drivers pre-installed, following Saika's best security and usability practices.
    3.  **Own Graphical Installer (Name in development):** A modern, accessible, guided installer that simplifies the Arch installation process without hiding advanced options.
    4.  **Saika Kernel (Optional):** A Linux kernel compiled with specific patches to improve interactive responsiveness (`linux-zen` as base) and support for experimental hardware.

**Maintenance Philosophy:** "Arch, with love and cohesion." Effort is focused on maintaining the Saika layer, not repackaging the entire Arch ecosystem.

---

## **4. Component: SaikaDesktop Environment (SDE)**

**Description:** The heart of the user experience. A dynamic desktop environment built from the ground up for Wayland, transforming based on task and device.

**Definitive Features:**
1.  **Three Unified Interface Modes:**
    *   **Wave Mode (Traditional/Floating):** Classic interface based on floating windows, optimized for mouse and keyboard precision.
    *   **Stream Mode (Dynamic Tiling):** Tiling window manager with intelligent and pre-configured layouts. Ideal for productivity and multitasking.
    *   **Touch Mode (Tablet/Touch):** Complete shell optimized for touch interaction, with gestures, on-screen keyboard (integrated `squeekboard`), and large controls.
2.  **Fluid Transition Between Modes:** The switch can be manual (keyboard shortcut, panel button) or automatic, triggered by the **Contextual System** upon detecting a screen rotation, connection of an input device, or a specific application.
3.  **Context System (Daemon "KAI"):** A background service that aggregates data from sensors (time, battery), hardware (connected devices), and software (focused window) to emit "context suggestions" (e.g., "It seems you are starting a video call, activate Focused Mode?").
4.  **Dynamic "Living" Themes:** The color scheme is not static. It can automatically derive from the main wallpaper, change smoothly throughout the day (from cool morning blue to warm evening orange), or react to system events.

**Proposed Tech Stack:**
*   **Compositor/Shell:** Developed in **Rust**, using the **Smithay** library (for finer control) or based on **Niri** (for the "scrollable tiling" concept). The user interface frontend (panels, launchers, overlays) will be built with **Slint** or **Qt Quick (QML)** for its declarative capabilities and excellent performance for animated interfaces.
*   **Protocol:** Native Wayland. No legacy X11 support (possibly via `XWayland` for compatibility).

---

## **5. Component: Saika Suite**

**Description:** A set of native applications, designed from scratch to integrate perfectly with SDE's philosophy and capabilities. It does not seek to replace the entire software stack, but to offer exemplary tools for core tasks.

**Flagship Applications (Names in development):**

| Project Name (Creature) | Application | Description and Differentiator |
| :--- | :--- | :--- |
| **KAI (System)** | Saika Control Center | The unified system configuration panel. Controls SDE, hardware, network, and **is the interface for the Context System (Daemon KAI)**, allowing creation and fine-tuning of automatic adaptation rules. |
| **RYU (Dragon)** | File Manager "Flow" | Adaptive file browser. Changes its layout and controls between SDE's three modes. Integrates tiling views, rich previews, and **semantic "Workspaces"** linked to SDE's workspaces. |
| **SHARK (Shark)** | Browser "Portal" | Not a new engine. It is a deep productivity and integration layer on top of **Firefox** or **Chromium**. Unifies the search bar with the system, allows grouping tabs into "sessions," and offers an overlaid reading/consultation mode on the desktop. |
| **KITSUNE (Fox)** | Connectivity Client "Link" | An app/daemon that unifies connection with other devices. Shares files, clipboard, and notifications between SaikaOS and Android/iOS (using KDE Connect as backend/inspiration), and allows using the phone as a media remote or presenter. |
| **PHOENIX (Phoenix)** | Integrated Terminal & Console | Modern terminal with support for inline graphics, panel splitting, contextual command completion, and a "scripting" mode to automate complex system and SDE tasks. |
| **OWL (Owl)** | Multimedia Viewer/Organizer "Noche" | Lightweight and fast image and video viewer. In Touch Mode, it becomes a touch gallery. In Stream Mode, it can display as a side preview panel. |

**Development Philosophy:** "Integration over Imitation." Deep connection with SDE and other Suite apps is prioritized over duplicating functions already excellent in the FOSS ecosystem (e.g., no video editor is planned, Kdenlive is recommended and integrated).

---

## **6. Component: Saika Display Kiosk & Orchestrator (SDKO)**

**Description:** More than a simple login manager (display manager). It is the orchestrator of the user session and the entry point to contextual profiles.

**Key Features:**
1.  **Modern Login Screen:** Minimalist graphical interface for user selection and password entry.
2.  **Profile/Scenario Selector:** Before logging in, the user can choose a pre-configured **"Scenario"** (e.g., "Deep Work", "Gaming", "Presentation", "Entertainment"). This scenario automatically loads SDE in the corresponding mode, opens predefined applications, and applies context rules.
3.  **Advanced Session Management:** Ability to save the session state (open windows and their arrangement) and restore it, linked to a profile or workspace.
4.  **Technical Implementation:** It will be an independent Wayland client, developed in **Qt Quick** for visual consistency and access to system libraries.

---

## **7. Technical Architecture and Tech Stack**

*   **Programming Languages:**
    *   **Rust:** For low-level components, critical for performance and security: SDE compositor core, system daemons (KAI), system tools.
    *   **C++ / QML (Qt):** For user applications in the Saika Suite that require the maturity and widget set of Qt (Control Center, File Manager).
    *   **Slint (Rust):** Actively evaluated as an alternative to QML for SDE UI and new apps, due to its native Rust integration and declarative model.
    *   **Python/Go:** For administration scripts, auxiliary tools, and the graphical installer.
*   **Graphics System:** **Wayland** (native protocol). X11 only via `XWayland`.
*   **Packaging System:** **pacman** + **makepkg**. All Saika components will be distributed as `.pkg.tar.zst` packages through SaikaOS repositories and the AUR.
*   **Version Control:** Git, organized on GitHub/GitLab under `SaikaNET-Studio`.
*   **CI/CD:** GitLab CI or GitHub Actions to automatically build packages with each commit, generate nightly ISO images, and run basic test suites.

---

## **8. Development Roadmap**

Development will follow a **vertical prototype strategy**, building a minimal functional flow before expanding.

**Phase 0: Foundation (Current - 3 months)**
1.  Establish the `SaikaNET-Studio` organization on GitHub/GitLab.
2.  Create base repositories with READMEs, licenses (GPL/LGPL where applicable), and vision documents.
3.  Configure a basic `archiso` profile that generates an ISO with Arch + XFCE + Saika visual theme (proof of concept).

**Phase 1: The Adaptable Core (SDE v0.1) (4 - 9 months)**
1.  Development of basic **SDKO** (login screen).
2.  Development of the **SDE compositor** in Rust (based on `niri` or `smithay`) with initial support for **Wave Mode (floating)**.
3.  Development of the **Context Daemon KAI** with basic rules.
4.  Integration: Ability to log in with SDKO to SDE in Wave Mode. **First demonstrable milestone.**

**Phase 2: Expansion and Suite (10 - 18 months)**
1.  Implement **Stream Mode (tiling)** and **Touch Mode (touch)** in SDE.
2.  Develop the first **Saika Suite** apps: **Control Center KAI** and **File Manager RYU**.
3.  Integrate the **Portal Browser SHARK** (as a deep extension/theme for Firefox).
4.  Publish packages in the AUR for advanced Arch users.

**Phase 3: SaikaOS and Polishing (19 - 30 months)**
1.  Unify all components into the **first alpha ISO of SaikaOS** with the graphical installer.
2.  Develop the remaining Suite tools (**KITSUNE, PHOENIX**).
3.  Alpha/beta closed testing cycle, UI/UX refinement, and extensive documentation.
4.  **Launch of SaikaOS 1.0 "Founding Bloom".**

---

## **9. Strategy, Community, and Sustainability**

*   **Development Model:** Open and community-driven from day one. RFCs (Request for Comments) will guide important technical decisions.
*   **Community:** An inclusive and technical community will be fostered on a self-hosted forum (Flarum/Discourse) and/or Matrix. Key contributors ("Founding Creatures") will be recognized in the system and documentation.
*   **SaikaNET Studio Sustainability:** As a non-profit entity, it will explore:
    *   Community donations (Open Collective, Patreon).
    *   Merchandise sales (t-shirts, stickers).
    *   Professional support, customization, and consulting services for companies wishing to use SaikaOS.
    *   Possible agreements with hardware manufacturers for sale of devices with SaikaOS pre-installed.
*   **Brand and Identity:** A strong and coherent visual identity (logo, color palette, typography, iconography) will be developed by community designers and applied across all components.

---
**Conclusion:** Project Saika is not just another operating system or desktop environment. It is an **ambitious experiment** to rethink how we interact with our computers, prioritizing adaptation, coherence, and intelligent choice over rigidity and fragmentation. The path is long and complex, but each step builds on the solid foundation of Arch Linux and the passion of a community that believes in a more fluid and personal computer.
