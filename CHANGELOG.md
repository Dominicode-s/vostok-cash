# Cash System — Changelog

### v2.8.0
- Added Signals API for mod developers (cash_sold, cash_bought, cash_dropped)
- Other mods can hook into cash transactions via Engine.get_meta("CashMain")
- Changed all MCM Float sliders to Int — sell rate now shown as percentage (e.g. 80 = 80%)
- Changed loot rarity from Int slider to Dropdown with labels (Common, Rare, Legendary)
- Existing MCM settings will reset to defaults on first launch

### v2.7.2
- Fixed MCM config crash when config keys are missing or corrupted
- Added signal disconnect in trade UI cleanup to prevent duplicate transactions

### v2.7.1
- Added null guards on get_node calls to prevent crashes
- Set focus_mode to NONE on injected buttons

### v2.5.0
- Euro Cash now spawns naturally in civilian and industrial loot containers (1–200€ per stack, Common rarity)
- Fixed stale icon cache — icon is now rebuilt fresh every launch, old CashIcon.tres auto-deleted
- Added resource cache busting on all user:// assets to prevent Godot serving stale data between mod updates
- General cleanup and conflict audit

### v2.3.0
- Custom 3D cash bundle model (euro note OBJ parsed at runtime) replaces the green box
- Custom transparent 128×128 inventory icon
- Unshaded rendering with desaturated colours to fit the game's dark aesthetic
- Graceful fallback to placeholder icon and green box if custom assets are missing

### v2.2.1
- Fixed in-world stacks sharing the same value — each dropped pile is now independent
- Place via right-click context menu now works correctly using vanilla ContextPlace

### v2.2.0
- Cash pickups now persist across save/reload
- Dropped cash can be picked up with G like other items

### v2.1.0
- Cash can now be dropped in the world as a physics object
- Improved stack handling for large amounts

### v2.0.0
- Major rework — converted from virtual wallet to physical inventory items
- Cash is now a stackable 1×1 inventory item (type: Valuables, zero weight)
- Sell items at traders for cash, buy items with cash
- Inventory header shows current cash total
- Automatic migration from v1.x — old wallet balance converts to physical cash on first load

### v1.2.2
- Added modworkshop update checking support — mod loader can now detect new versions

### v1.2.1
- Fixed barter trading being blocked when Cash mod is active — wallet UI container was intercepting mouse events on the Accept/Reset buttons

### v1.2.0
- Added Mod Configuration Menu (MCM) integration — sell rate and death reset configurable via MCM
- Added Metro/Community Mod Loader support
- Death reset is now configurable (on by default)
- Settings gracefully fall back to defaults if MCM is not installed

### v1.0.0
- Initial release
- Virtual wallet system for traders (sell items for €, buy items with €)
- Wallet badge displayed in inventory header alongside Capacity/Weight/Value
- Compact single-row trade UI with Sell/Buy buttons and flash feedback
- Wallet persists across sessions, resets on death
- Fully compatible with both XP & Skills System and Economy Overhaul mods
- Uses zero script overrides — pure autoload with dynamic UI injection
