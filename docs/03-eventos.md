# 3. Dialogue Events with Blueprint Interfaces

[← Back to README](../README.md)

**Available in Free and Full.** The system can trigger gameplay actions from conversation rows using **`BPI_DialogueEvents`**. Turn lights on, open doors, or change gameplay variables without modifying the dialogue component's core logic.

## How `AC_Dialogue` Sends Messages

The component's Event Graph shows the following flow when a row has `Type = Event`:

1. **`Switch on E_DialogueType`** follows its `Event` output.
2. **`Get All Actors with Interface`** finds Actors implementing `BPI_DialogueEvents`.
3. **`For Each Loop`** iterates over the matching Actors.
4. **`Execute Dialogue Event`** sends an interface message to each Actor, using `Array Element` as its `Target`.
5. **`Dialogue Current Event`** is passed to the message's `Event Name` parameter; this is the event identifier configured for the dialogue row.

```text
AC_Dialogue · Switch on E_DialogueType
              └── Event
                  └── Get All Actors with Interface (BPI_DialogueEvents)
                      └── For Each Loop
                          └── Execute Dialogue Event (Message)
                              Target     = Array Element
                              Event Name = Dialogue Current Event
```

**Important:** Messages are sent to **all matching Actors implementing the interface**, not just one selected by the event name. Each receiver should filter incoming event identifiers and respond only to the relevant ones.

### Sending Events from AC_Dialogue

The `AC_Dialogue` component uses `Get All Actors with Interface` to find Actors implementing `BPI_DialogueEvents`. It iterates over them using `For Each Loop` and calls `Execute Dialogue Event`, passing the value stored in `Dialogue Current Event`.

![Sending events from AC_Dialogue](https://raw.githubusercontent.com/wohostudios/ue5-dialogue-system-starter-pack-es/main/images/switch.png)

## Step 1. Configure the Event in a Data Table

1. Open your Data Table based on `ST_DialogueLine`.
2. Create or select a row that should trigger an action.
3. Set **`Type`** to **`Event`**.
4. Enter an event identifier in **`TriggerEvent`** (type `Name`), such as `PowerActivate`.
5. Configure any other required properties and save the table.

> The value of `TriggerEvent` must exactly match the corresponding case in `Switch on Name`. `Type = Event` is important because that is the branch that sends interface messages.

## Step 2. Prepare a Receiving Actor

You can use your **player Blueprint**, a **door or mechanism Actor**, or any other Actor that should react to the conversation. The demonstration also shows an implementation in the **Level Blueprint**.

1. Open the receiving Actor Blueprint.
2. Go to **Class Settings → Interfaces → Implemented Interfaces**, then click **Add**.
3. Choose **`BPI_DialogueEvents`**.
4. Compile and save.
5. In the Event Graph, add **`Event ExecuteDialogueEvent`**.
6. Connect its execution pin to **`Switch on Name`**, and its **`Event Name`** output to **`Selection`**.
7. Add cases for the event names the Actor should handle.

```text
Event ExecuteDialogueEvent (from BPI_DialogueEvents)
    Exec ───────────────────► Switch on Name
    Event Name ─────────────► Selection
                                ├── PowerActivate → Turn on light
                                ├── PowerOff      → Turn off light
                                └── OpenDoor      → Custom door logic
```

**You do not need to manually target the receiver from `AC_Dialogue`:** the component finds Actors implementing the interface and sends them the message. Ensure the receiving Actor exists in the world when the event is sent.

## Example A. Turn a Light On or Off (Level Blueprint)

The example project uses a reference to `PointLightFacility`, its `Point Light Component`, and a Timeline called `TL_LightFade`.

- **`PowerActivate`**: plays `TL_LightFade`. Its `Update` output calls `Set Intensity` using the Timeline's `Intensity` value.
- **`PowerOff`**: calls `Set Intensity` with `New Intensity = 0`.

This demonstrates how a conversation event controls a level element. If recreating the setup in another map, verify that your receiver is discovered by `Get All Actors with Interface`.

### Light Control Example

The Level Blueprint receives `Event ExecuteDialogueEvent`. `Switch on Name` determines which action to perform.

![Level Blueprint dialogue events — first view](https://raw.githubusercontent.com/wohostudios/ue5-dialogue-system-starter-pack-es/main/images/eventos-level-blueprint1.png)
![Level Blueprint dialogue events — second view](https://raw.githubusercontent.com/wohostudios/ue5-dialogue-system-starter-pack-es/main/images/eventos-level-blueprint2.png)

## Example B. Change a Player Variable

In `BP_FirstPersonCharacter`, with `BPI_DialogueEvents` added to **Implemented Interfaces**, `Event ExecuteDialogueEvent` uses `Switch on Name`:

- **`ActiveTrigger`**: `Set MovePlayer = true`.
- **`OpenDoor`**: `Set MovePlayer = false`.

These are **example event names and behaviors from the demo project**. Use identifiers matching your own Data Table rows. In this screenshot, `OpenDoor` changes a Boolean variable; **it does not open a door by itself**.

### Receiving Events in the Player

Implement `BPI_DialogueEvents` in your character Blueprint and use `Switch on Name` to respond to each event.

![Receiving dialogue events in the player character](https://raw.githubusercontent.com/wohostudios/ue5-dialogue-system-starter-pack-es/main/images/eventos-player-character.png)

## Troubleshooting Event Delivery

1. Ensure the conversation reaches a row with `Type = Event` and a defined `TriggerEvent`.
2. Check that the event name exactly matches a `Switch on Name` case.
3. Verify that the receiver **implements** `BPI_DialogueEvents`, is loaded, and exists in the world.
4. Temporarily add `Print String` to `Event ExecuteDialogueEvent` to confirm that it fires.
5. If the event arrives but nothing happens, inspect the logic after the Switch and component references.
6. If multiple Actors react unexpectedly, remember that the message is broadcast to all matching interface implementers; filter by name inside each Actor.
