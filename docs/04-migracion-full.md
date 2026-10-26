# 4. Upgrading from Starter Pack (Free) to Framework (Full)

[← Back to README](../README.md)

> **Start Free. Upgrade Anytime. Keep Your Conversations.**

Both editions use compatible conversation Data Tables. If you already created dialogues in Free, **you can keep them when upgrading** to Full.

## What You Can Keep

- Conversation Data Tables based on `ST_DialogueLine`.
- Row names, ordering, and entered dialogue text.
- Previously configured event identifiers, provided you preserve the receivers and their setup.

## Step-by-Step Migration

1. **Back up** your project before importing the new edition.
2. Add **Dialogue System Framework (Full)** to your project using the Fab package.
3. Keep the conversation Data Tables you created in Free.
4. In your player Blueprint, use the Full edition's dialogue Actor Component.
5. Initialize the Full dialogue interface according to its documentation and connect your existing Data Tables to the corresponding playback function.
6. Test a conversation to verify text, ordering, timing, and events.
7. Configure any new Full features you want (decisions, Rich Text, localization, voice-over, or UI layouts).

**Important when importing:** if Unreal Engine asks to overwrite assets with the same names, do not accept automatically. Keep backups and verify that your Data Tables reference the correct structure in your installed edition.

You do not need to retype your conversations. The exact asset migration steps may require checking references depending on how both editions were imported.

## Free vs Full

| Feature | Free | Full |
|---|:---:|:---:|
| Player Actor Component | ✅ | ✅ |
| Conversation Data Tables | ✅ | ✅ |
| Sequential dialogue | ✅ | ✅ |
| Events with Blueprint Interfaces | ✅ | ✅ |
| `Duration` and `DelayAfter` | ✅ | ✅ |
| Multiple dialogue UIs | — | ✅ |
| Common UI decision system | — | ✅ |
| Data Table-driven dialogue choices | — | ✅ |
| Rich Text with colored words | — | ✅ |
| Synchronized voice-over | — | ✅ |
| English/Spanish localization | — | ✅ |
| `AllowSkip` | — | ✅ |

## Where Can I Get Full?

**[Dialogue System Framework (Full) on Fab](https://www.fab.com/listings/e6c1f535-2990-4551-8303-c3405ebd7aad)** — reference price provided by the developer: **USD 14.99** (check Fab for the current price).

The Free edition remains free and useful on its own. Upgrading is entirely optional.
