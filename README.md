# SuperClassicPlayBot 🎮

**A production-grade Telegram gaming platform featuring 35+ games, a virtual economy, Telegram WebApp integration, and a clean modular Python architecture built on aiogram 3.x.**

> [!NOTE]
> This is a **showcase repository** — documentation, architecture overview, and feature catalogue for the private `SuperClassicPlayBot` engine.

---

## 💎 Engineering Excellence

- **80+ automated tests** (Pytest) — unit, integration, and game-engine stress tests.
- **Full state persistence** via Redis — bot restarts never lose active game sessions.
- **CI/CD** — GitHub Actions runs Ruff + mypy linting and the full test suite on every PR.
- **Clean Architecture** — strict separation: Telegram handlers / game engines (`core/games/`) / service layer (`core/services/`).
- **Async-first** — `asyncio` throughout, SQLAlchemy 2.0 async ORM, aiogram 3.x.
- **Telegram WebApp** — React + Vite + TypeScript frontend for rich in-browser games (Chess, Match-3, Mahjong, Battleship, Gartic Phone, Voxel Editor, Build Battle).
- **Prometheus metrics** — built-in `/metrics` endpoint for production monitoring.
- **i18n** — flat YAML locale files, full Ukrainian & English support.

---

## 🎮 Games Catalogue (35+)

### 🃏 Card Games
Durak (Classic & Pro) · Blackjack · Poker · Bridge · Thousand · Ochko · Scopa · High-Low · War

### ♟️ Board & Strategy
Chess *(WebApp)* · Checkers · Reversi · Gomoku · Connect Four · Minesweeper · Backgammon · Battleship *(WebApp)* · Breakthrough · Domino

### 🧩 Casual & Creative
Match-3 *(WebApp)* · Mahjong *(WebApp)* · Voxel Editor *(WebApp)* · Build Battle *(WebApp)* · Gartic Phone *(WebApp)* · Gallows · Bulls & Cows · Words · Kobza

### 🎯 Quiz & Knowledge
Guess the Flag · Italian Quiz / Signs / Words · Stalker Quiz · Music Quiz · Custom Quiz · Genshin

### 🎰 Mini-games
Casino · Kinder · Cplay (inline)

---

## 💰 Virtual Economy

- **Currencies**: Gold 💰 · Gems 💎 · Bitcoin ₿ · Toncoin
- **Shop**: Phones · Cars · Houses · Yachts · Businesses · Mining Farms · Power Plants
- **Passive income**: businesses → hourly gold; farms → BTC; power plants → energy
- **Social**: clans, RP commands, rich profiles with stats & avatar

---

## 📁 Architecture

```mermaid
graph TD
    User((User)) <--> TG[Telegram API]
    TG <--> Handlers[Handlers Layer]
    Handlers <--> Svc[Core Services]
    Svc <--> Redis[(Redis — State)]
    Svc <--> Engine[Game Engines]
    Engine <--> DB[(PostgreSQL / SQLite)]
    User <--> WebApp[Telegram WebApp\nReact + Vite]
    WebApp <--> Svc

    subgraph "Core"
        Engine
        Svc
    end
```

```
SuperClassicPlayBot/
├── src/
│   ├── bot/                    # Entry point, startup/shutdown, Prometheus
│   ├── core/
│   │   ├── models/             # SQLAlchemy models (User, Inventory, …)
│   │   ├── services/           # UserService, EconomyService, GameService …
│   │   ├── games/              # 35+ game engines
│   │   │   ├── base/           # Card, Deck, LobbyManager, GameEngine
│   │   │   ├── chess/ durak/   # Engine examples
│   │   │   └── …
│   │   ├── middleware/         # Auth, throttling, i18n
│   │   └── uikit/              # GamePresenter, shared UI components
│   └── handlers/
│       ├── economy/            # Shop, bonuses, inventory
│       ├── games/              # One handler module per game
│       ├── admin/              # Admin panel
│       └── social/             # Clans, RP
├── webapp-client/              # React + Vite + TypeScript WebApp
│   └── src/games/
│       ├── Chess · Match3 · Mahjong
│       ├── Battleship · GarticPhone
│       └── VoxelEditor · BuildBattle
├── locales/                    # i18n YAML (uk, en)
├── tests/                      # Pytest test suite (80+ tests)
├── .github/workflows/          # CI/CD
└── docker-compose.yml
```

---

## 🛠️ Tech Stack

| Layer | Technology |
|-------|------------|
| Bot framework | aiogram 3.24 |
| ORM | SQLAlchemy 2.0 async |
| Migrations | Alembic |
| State | Redis 5.x |
| Image processing | Pillow · rembg |
| Chess | python-chess |
| WebApp | React 18 + Vite + TypeScript |
| Linting | Ruff · mypy |
| Testing | Pytest · pytest-asyncio |
| Monitoring | Prometheus |
| Container | Docker + docker-compose |

---

## 📄 License

MIT

---

*Built with ❤️ — 35+ games, full economy, WebApp integration.*


---

## 💎 Engineering Excellence

This project is built using modern Python development best practices:

*   **Robust Test Suite**: Covered with **80+ automated tests** (Pytest), including Unit testing, integration tests for Telegram handlers, and stress tests for the card engine.
*   **State Persistence**: All active games are persistent via **Redis**. The bot can restart at any moment without players losing their active game state.
*   **CI/CD Pipeline**: GitHub Actions are set up for automated testing (Linting + Testing) on every Pull Request.
*   **Clean Architecture**: Separation between the Telegram interface layer (`handlers/`), game business logic engines (`core/games/`), and DB service layer (`core/services/`).
*   **Performance First**: Built fully asynchronously (`asyncio`) and using optimized DB queries via SQLAlchemy 2.0.
*   **Multilingual**: Full support for 🇺🇦 Ukrainian and 🇬🇧 English via YAML localization files.

---

## ✨ Features & Modules

### 💰 Virtual Economy & Shop
- **Currency System**: Custom economy featuring multiple currencies (Gold, Gems, Bitcoin, Toncoin).
- **Interactive Shop**: Ability to buy, own, and sell assets across categories:
  - *Phones* (from Nokia 3310 to iPhone 15 Pro Max)
  - *Cars* (Audi Q7, BMW X6, Mercedes S63, Rolls-Royce)
  - *Houses* (Apartments, Villas, Mansions, Mars base)
  - *Yachts* (Bavaria 40, Princess 60, Eclipse)
- **Passive Income & Mining**: Purchase businesses (Cafes, Nightclubs) and mining farms (TI-Miner, Saturn) to generate hourly income.
- **Power Plants**: Build Wind, Solar, or Nuclear power plants to manage and sell energy.
- **Daily Bonuses & Inventory**: Interactive player profiles and item management.

### 🎮 Premium Card Game Engines
- **Universal Card System**: Fully modular deck, card, and hand representation that can be reused for any card game.
- **Lobby Manager**: Handles game matchmaking and supports adding/removing AI bots to fill lobbies with one click.
- **Durak (Дурень) Engine**:
  - Classic & Pro rules supported.
  - Custom game timers for turns (FSM).
  - *Cheating mechanics*: Allows players to sneak cards out of turn with a risk of getting caught by others clicking the "🤡 Caught Cheating!" button.
  - *Visual enhancements*: Inline player tags placed next to cards on the active table message.
  - Auto-cleanup of chat messages to keep groups tidy.

---

## 📁 Architecture & Directory Layout

```mermaid
graph TD
    User((User)) <--> TG[Telegram API]
    TG <--> Handlers[Handlers Layer]
    Handlers <--> Lobby[Lobby Manager]
    Lobby <--> Redis[(Redis Persistence)]
    Lobby <--> Engine[Game Engines core/games]
    Engine <--> DB[(PostgreSQL/SQLite)]

    subgraph "Core Logic"
        Engine
        Lobby
    end
```

```
ClassicPlayBot/
├── bot/                   # entry point
├── core/                  # Business logic
│   ├── models/            # User, Inventory, Assets models
│   ├── services/          # UserService, EconomyService
│   └── games/             # Game Engines
│       ├── base/          # Card, Deck, LobbyManager base classes
│       └── durak/         # Durak game loop & logic
├── handlers/              # Telegram handlers & controllers
│   ├── start.py           # Start handler
│   ├── economy/           # Shop, Inventory, Bonuses handlers
│   └── games/             # Durak interface handlers
├── database/              # SQLAlchemy models & migrations
└── config/                # Items list, localizations, settings
```

---

## 🎯 Ready for Web Integration

The game and economy core logic are completely decoupled from Telegram and the `aiogram` API. This architecture makes it extremely easy to scale:
- ✅ Telegram bot interface.
- 🔄 FastAPI REST API (can be plugged directly into `core/`).
- 🔄 WebSockets for real-time multiplayer browser play.

```python
# The same core logic works anywhere!
from core.games.durak.engine import DurakEngine

# Current Telegram lobby
game = DurakEngine(game_id, creator)

# Future FastAPI WebSocket route
@app.websocket("/ws/durak/{game_id}")
async def durak_websocket(websocket: WebSocket, game_id: str):
    # Uses the exact same DurakEngine instance!
    ...
```

---

## 🛠️ Stack & Technologies

*   **Python 3.11+**
*   **aiogram 3.15** (Telegram framework)
*   **SQLAlchemy 2.0** (Async ORM)
*   **Redis** (State persistence)
*   **Pytest** (Testing suite)
