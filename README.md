# Rain Jungle - Metroidvania Z-Fighter Engine

> A dual-scene Unity 2D Metroidvania featuring dedicated fighting-game arena transitions, dynamic branching dialogue tied to equipment state, and a robust data-driven architecture.

---

## **Project Overview**

**Rain Jungle** combines two distinct gameplay loops into a unified, modular architecture:
1. **Exploration (Overworld / Metroidvania):** Side-scrolling platforming, environmental traversal, NPC interactions, and narrative progression.
2. **Combat Arena (Z-Fighter Style):** Dedicated 1VS1 combat scenes triggered upon encountering enemies or bosses, featuring intense aerial physics and combo-focused mechanics.

---

## **Core Architecture & Design Patterns**

*   **Dual-Scene Architecture:** Manages persistent global state via a centralized `GameManager` (`DontDestroyOnLoad`), seamlessly switching between the Exploration world and the Combat Arena without losing player progress, inventory, or equipment stats.
*   **Data-Driven Design (ScriptableObjects):** All static content—including clothing items, stats, and dialogue trees—is decoupled from logic and managed via editable ScriptableObjects (`ClothingData`, `DialogueData`), allowing instant balancing without code changes.
*   **Observer Pattern (Event Channels):** Decouples decoupled systems (UI, audio, inventory, and combat) using ScriptableObject-based event channels (`VoidEventChannelSO`, `ItemEventChannelSO`) to prevent direct script dependencies.
*   **State Machine:** Manages complex behaviors for players and enemies across distinct states (`IdleState`, `RunState`, `AttackState`, `HurtState`), eliminating massive nested conditional blocks.
*   **Service Locator:** Lightweight registry pattern used strictly for global cross-cutting services like audio, saving, and scene loading.
*   **Model-View-Presenter (MVP):** Strictly separates UI rendering (`View`), internal state variables (`Model`), and event coordination (`Presenter`) for elements like inventories and dialogue boxes.
*   **Strategy Pattern (Dialogue Conditions):** Evaluates branching dialogue options dynamically using modular condition strategies (e.g., checking if the player has a specific clothing item equipped).

---

## **Project Directory Structure**

The project relies on a strict **Feature-Driven** layout located inside a single root folder to isolate source assets from third-party plugins:

```text
Assets/
│
├── _Project/
│   ├── Animations/
│   ├── Art/
│   │   ├── Sprites/
│   │   │   ├── Characters/
│   │   │   ├── Environment/
│   │   │   └── UI/
│   │   └── Materials/
│   │
│   ├── Audio/
│   │   ├── Music/
│   │   └── SFX/
│   │
│   ├── Prefabs/
│   │   ├── Environment/
│   │   ├── Characters/
│   │   ├── World/
│   │   └── UI/
│   │
│   ├── Scenes/
│   │   ├── Core/
│   │   ├── World/
│   │   └── CombatArena/
│   │
│   ├── ScriptableObjects/
│   │   ├── Dialogues/
│   │   ├── Items/
│   │   │   └── Clothing/
│   │   ├── Characters/
│   │   └── Combat/
│   │
│   └── Scripts/
│       ├── Core/
│       ├── Exploration/
│       ├── Combat/
│       ├── Dialogue/
│       ├── Inventory/
│       ├── UI/
│       └── Utils/
│
└── ThirdParty/