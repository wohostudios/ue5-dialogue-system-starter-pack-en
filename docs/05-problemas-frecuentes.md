# 5. Frequently Asked Questions & Troubleshooting

[← Back to README](../README.md)

### My Conversation Does Not Start

Check that the player has `AC_Dialogue`, that `Dialogue Create Widget` runs before `Dialogue Play Conversation`, that both nodes have `AC_Dialogue` connected to `Target`, and that `Conversation` is assigned a valid Data Table.

### The Dialogue Runs, but I Cannot See the Interface

Make sure `Dialogue Create Widget` has been executed. Check the order of the nodes and confirm you are using the player character that actually owns the component.

### Dialogue Lines Appear in the Wrong Order

Inspect the `Order` values of every row. Remember that `Row Name` and `Order` are different fields.

### A `TriggerEvent` Does Not Work

Verify the exact event name, the implementation of `BPI_DialogueEvents`, the `Switch on Name` cases, and the receiving Actor. See [Dialogue Events](03-eventos.md). The interface must be implemented by an Actor that exists in the world when the event is sent.

### `AllowSkip` Exists but Does Nothing

This is expected: **configurable skipping per line is exclusive to Full**. The field is present in Free to maintain `ST_DialogueLine` compatibility.

### I See `Audio_EN`, `Audio_ES`, and `Text_ES`. Does Free Include Voices and Localization?

No. These columns are retained as part of the shared structure. Advanced voice-over and localization functionality is exclusive to Full.

### Can I Use the System with First Person or Third Person Templates?

Yes. Add `AC_Dialogue` to your character Blueprint and call the functions described in the [installation guide](01-instalacion.md). The interaction event used to start dialogue may vary between templates.

### Do I Need to Replace My `GameInstance`?

No. Both editions use an Actor Component and do not require the old `BP_DialogueGameInstance`.

### Will I Lose My Dialogues When I Upgrade to Full?

You do not need to recreate your conversations: the Data Tables are compatible. Back up your project and import Full carefully to preserve your existing assets. See [Upgrading to Full](04-migracion-full.md).

### Where Can I Get Help?

[Spanish-speaking support Discord](https://discord.gg/JY5JTQaWqn) · [Free Starter Pack on Fab](https://www.fab.com/listings/1d39c10d-b6b0-4dd1-b704-8b3d60658e23)
