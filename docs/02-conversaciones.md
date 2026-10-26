# 2. Creating Conversations with Data Tables

[← Back to README](../README.md)

## How Does It Work?

Each Data Table stores a conversation. Each row represents a dialogue line or an instruction. Data Tables use **`ST_DialogueLine`**, the structure shared with the Full edition to make upgrading easier.

## Create a New Data Table

1. In the **Content Browser**, choose a folder for your conversations.
2. Right-click → **Miscellaneous → Data Table**.
3. Choose **`ST_DialogueLine`** as the row structure.
4. Name the asset, for example `DT_FirstConversation`.
5. Open it, click **Add**, and configure each row in **Row Editor**.
6. Save the Data Table.

### Row Name vs. Order

- **Row Name** identifies a row within the Data Table (for example, `001`, `002`, `003`).
- **Order** is the numeric field intended to determine dialogue sequence (for example, `0`, `1`, `2`).

These are different values. For sequential dialogue, use consistent `Order` values without duplicates.

## `ST_DialogueLine` Fields

| Field | Observed Type | Purpose / Availability |
|---|---|---|
| `Order` | Integer | Dialogue line order. |
| `DisplayType` | Enum (`E Dialogue Display…`) | Display setting; this does not mean multiple UIs are included in Free. |
| `Type` | Enum (`E Dialogue Type…`) | Row type; the demo uses `Normal`, `Event`, and `Input`. |
| `Speaker` | Name | Speaker identifier. |
| `ShowSpeaker` | Boolean | Whether to display the speaker's name. |
| `Text_EN` | Text | English dialogue text field. |
| `Text_ES` | Text | Spanish dialogue text field. |
| `Audio_EN` | Sound Base | Audio field; voice functionality is exclusive to Full. |
| `Audio_ES` | Sound Base | Audio field; voice functionality is exclusive to Full. |
| `Duration` | Float | Line duration in seconds. **Free and Full.** |
| `DelayAfter` | Float | Delay after the line in seconds. **Free and Full.** |
| `TriggerEvent` | Name | Gameplay event identifier. **Free and Full.** |
| `AllowSkip` | Boolean | Per-line skip control, **Full only**. Has no effect in Free. |
| `PromptText_EN` | Text | English contextual prompt; confirm functionality in Free before relying on it. |
| `PromptText_ES` | Text | Spanish contextual prompt; confirm functionality in Free before relying on it. |

> **Compatibility does not mean feature availability:** `ST_DialogueLine` contains properties not processed by Free. Do not delete fields or change their types: they are retained so your conversations can be reused in Full. The presence of `Text_ES`, `Audio_EN`, and `Audio_ES` does not mean localization or voice-over are enabled in Free.

The `ST_DialogueLine` structure contains the properties used to configure conversation lines.

![ST_DialogueLine structure](https://raw.githubusercontent.com/wohostudios/ue5-dialogue-system-starter-pack-es/main/images/st-dialogue-line.png)

## Basic Conversation Example

| Row Name | Order | Type | Speaker | Text_EN | Duration | DelayAfter |
|---|---:|---|---|---|---:|---:|
| `001` | 0 | Normal | Guide | Welcome to the facility. | 3.0 | 0.5 |
| `002` | 1 | Normal | Guide | Something has gone wrong. | 4.0 | 0.5 |
| `003` | 2 | Normal | Guide | Find the generator. | 3.0 | 0.5 |

This example uses normal sequential dialogue with English text. Adjust line durations for readability.

Each Data Table row represents a dialogue line or an instruction.

![Configuring a conversation Data Table](https://raw.githubusercontent.com/wohostudios/ue5-dialogue-system-starter-pack-es/main/images/tabla-conversacion.png)

## Timing and Delays

- `Duration = 4.0`: the configured line duration is four seconds.
- `DelayAfter = 0.5`: after that line, the system waits an additional half-second according to its playback logic.

Both properties work in Free and Full.

## Trigger Events

In `TriggerEvent`, enter an identifier such as `PowerActivate`. The receiving Blueprint uses this name to select an action. See the [events guide](03-eventos.md).

## Play Your Data Table

In the player Blueprint, after calling `Dialogue Create Widget`, call `Dialogue Play Conversation`, use `AC_Dialogue` as the `Target`, and select your new Data Table in `Conversation`.
