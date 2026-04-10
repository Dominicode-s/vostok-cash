# Cash System

Adds a physical Euro currency to Road to Vostok. Sell items at traders for cash, spend it to buy gear, and find cash scattered in loot containers across the world. Cash is a real inventory item - it takes up a slot, can be dropped, placed, picked up, and persists across saves.

Fully backward compatible with all previous versions. If you're upgrading from v1.x, your old wallet balance automatically converts to physical cash items on first load.

## Features

- Physical cash items - stackable 1×1 inventory items with custom 3D model and icon
- Sell selected items at any trader for cash, buy items using your cash balance
- Cash spawns naturally in civilian and industrial loot containers
- Drop, place, pick up, and stack cash like any other item in the game
- Dropped cash persists across save/reload
- Lose all cash on death (configurable)
- MCM support - configure sell rate and death behaviour via Mod Configuration Menu (optional)
- Inventory badge shows your total cash in the inventory header

## Compatibility

- Works alongside Economy Overhaul, XP & Skills System, and other mods
- Requires Metro/Community Mod Loader

## Installation

Drop `Cash-System.vmz` into your `mods/` folder and launch the game.

## Configuration

With MCM installed, find "Cash System" in the mod config menu:
- **Sell Rate** - fraction of item value received when selling (default: 80%)
- **Death Resets Cash** - remove all cash on death (default: on)

Without MCM, settings are saved automatically with defaults.

## For Mod Developers — Signals API

Other mods can hook into cash transactions using signals. Access the Cash System autoload via `Engine.get_meta("CashMain")` — returns `null` if Cash System isn't installed, so it's safe to use as an optional dependency.

```gdscript
func _ready():
    await get_tree().create_timer(1.0).timeout
    var cash = Engine.get_meta("CashMain", null)
    if !cash:
        return
    cash.cash_sold.connect(_on_sold)
    cash.cash_bought.connect(_on_bought)
    cash.cash_dropped.connect(_on_dropped)

func _on_sold(amount: int, items: Array):
    # amount = € earned, items = inventory elements that were sold

func _on_bought(amount: int, items: Array):
    # amount = € spent, items = supply elements that were bought

func _on_dropped(amount: int):
    # amount = € value of the dropped stack
```

| Signal | Args | Description |
|--------|------|-------------|
| `cash_sold` | `amount: int, items: Array` | Player sold items at a trader |
| `cash_bought` | `amount: int, items: Array` | Player bought items from a trader |
| `cash_dropped` | `amount: int` | Player dropped a cash stack |
