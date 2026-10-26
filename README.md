# Dialogue System — Starter Pack (Free)

A free dialogue system for Unreal Engine 5 · 100% Blueprints · Actor Component · Data Tables

Build sequential conversations, display dialogue on screen, and trigger gameplay actions through Blueprint Interfaces. This Starter Pack is designed for learning, prototyping, and adding dialogue to your own projects.

> **Start Free. Upgrade Anytime. Keep Your Conversations.**
>
> Conversation Data Tables created with this edition are compatible with **Dialogue System Framework (Full)**. To upgrade, keep your existing Data Tables and connect them to the Full edition's dialogue component. You do not need to rewrite your conversations.

[**Try the playable demo (MEGA)**](https://mega.nz/file/VjxkjD6R#zBJXSqZcaMePbTdpOoSafXH3vYIR1wc4s2NQn0zwyWk) · [**Get the free Starter Pack on Fab**](https://www.fab.com/listings/1d39c10d-b6b0-4dd1-b704-8b3d60658e23) · [**View the Full Framework on Fab**](https://www.fab.com/listings/e6c1f535-2990-4551-8303-c3405ebd7aad)

## Documentation

1. [Installation & quick start](docs/01-instalacion.md)
2. [Creating conversations & Data Tables](docs/02-conversaciones.md)
3. [Gameplay events using Blueprint Interfaces](docs/03-eventos.md)
4. [Free vs Full and upgrading](docs/04-migracion-full.md)
5. [FAQ & troubleshooting](docs/05-problemas-frecuentes.md)

## Free Edition Features

- Sequential dialogue system driven by Data Tables.
- 100% Blueprint implementation — no C++ required.
- `AC_Dialogue` Actor Component added directly to the player Blueprint.
- No need to replace your `GameInstance`, `GameMode`, or `PlayerController`.
- Speaker names and an included dialogue UI.
- Line timing (`Duration`) and delay after each line (`DelayAfter`).
- Gameplay events using `BPI_DialogueEvents` and `TriggerEvent`.
- A data structure designed for upgrading to the Full edition.

The component is designed to integrate with common Unreal Engine templates, including First Person and Third Person. Input setup and integration may vary depending on the template; see the [installation guide](docs/01-instalacion.md).

## Your First Conversation in Three Steps

1. Add `AC_Dialogue` to your character Blueprint.
2. On `BeginPlay`, call `Dialogue Create Widget`, using `AC_Dialogue` as the `Target`.
3. Call `Dialogue Play Conversation`, using the same `Target`, and select your Data Table in the `Conversation` pin.

```text
Event BeginPlay
    └─ Dialogue Create Widget  (Target: AC_Dialogue)
        └─ Dialogue Play Conversation  (Target: AC_Dialogue)
            └─ Conversation: your Data Table
```

This example starts a conversation automatically when the level begins. In a game, you can trigger conversations using another event, such as interacting with an NPC.

## Free vs Full

| Feature | Free | Full |
|---|:---:|:---:|
| 100% Blueprints | ✅ | ✅ |
| Data Table-driven conversations | ✅ | ✅ |
| Speaker names | ✅ | ✅ |
| Sequential dialogue | ✅ | ✅ |
| Events via Blueprint Interfaces | ✅ | ✅ |
| `Duration` / `DelayAfter` | ✅ | ✅ |
| Actor Component — no custom GameInstance | ✅ | ✅ |
| Compatible Data Tables for Free → Full migration | ✅ | ✅ |
| Multiple dialogue UI layouts | — | ✅ |
| Common UI decision system | — | ✅ |
| Data Table-driven dialogue choices | — | ✅ |
| Rich Text: colored highlighted words | — | ✅ |
| Voice-over and audio synchronization | — | ✅ |
| English/Spanish localization | — | ✅ |
| Per-line configurable skipping (`AllowSkip`) | — | ✅ |

**Important:** `ST_DialogueLine` contains fields used by the Full edition even when their functionality is unavailable in Free. These fields are retained for compatibility. See the [field reference](docs/02-conversaciones.md).

### When Should You Upgrade?

When your game needs interactive decisions, Rich Text, alternative dialogue layouts, synchronized audio, or localization, upgrade without recreating your conversation Data Tables.

[**Explore Dialogue System Framework (Full) on Fab**](https://www.fab.com/listings/e6c1f535-2990-4551-8303-c3405ebd7aad)

## Playable Demo

[**Download the playable demo on MEGA**](https://mega.nz/file/VjxkjD6R#zBJXSqZcaMePbTdpOoSafXH3vYIR1wc4s2NQn0zwyWk). The demo lets you try the system before adding it to a project. It is optional and does not replace the Unreal Engine package distributed through Fab. Verify the downloaded build on a clean machine before advertising definitive platform requirements.

## Support

- [Spanish-speaking Discord community](https://discord.gg/JY5JTQaWqn)
- [Free Starter Pack on Fab](https://www.fab.com/listings/1d39c10d-b6b0-4dd1-b704-8b3d60658e23)
- [Documentación en español](https://github.com/wohostudios/ue5-dialogue-system-starter-pack-es)
