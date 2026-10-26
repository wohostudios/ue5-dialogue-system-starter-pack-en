# 1. Installation & Quick Start

[← Back to README](../README.md)

## Requirements

- Unreal Engine 5, using a version supported by the package downloaded from Fab.
- A project with a player Blueprint or an Actor representing the system's user.
- The **Dialogue System — Starter Pack (Free)** added to your project from Fab.

No C++ or custom `GameInstance` is required.

## Step 1. Locate `AC_Dialogue`

In the **Content Browser**, navigate to:

`Content/DialogueSystem/Blueprints/Core/AC_Dialogue`

This Actor Component provides the functions used to create the dialogue interface and start conversations.

## Step 2. Add the Component to the Player

1. Open your player Blueprint, such as `BP_FirstPersonCharacter` or `BP_ThirdPersonCharacter`.
2. In **Components**, select **Add**.
3. Search for and select `AC_Dialogue`.
4. Compile and save the Blueprint.

The component will appear as `AC_Dialogue` in your player's component hierarchy (its graph reference may be labeled `AC Dialogue`).

## Step 3. Create the Dialogue Widget

1. Open the player's **Event Graph**.
2. Add `Event BeginPlay`.
3. Drag an `AC_Dialogue` reference from the Components panel into the graph.
4. From that reference, create `Dialogue Create Widget`.
5. Connect `BeginPlay` to the execution input of `Dialogue Create Widget`.
6. Connect `AC_Dialogue` to the `Target` pin.

## Step 4. Start a Conversation

1. From `AC_Dialogue`, create `Dialogue Play Conversation`.
2. Connect the execution output of `Dialogue Create Widget` to `Dialogue Play Conversation`.
3. Connect the same `AC_Dialogue` reference to the second function's `Target` pin.
4. In the **`Conversation`** pin, select the Data Table containing your conversation.
5. Compile, save, and play the level.

```text
Event BeginPlay
       │
       ▼
Dialogue Create Widget ◀── AC_Dialogue (Target)
       │
       ▼
Dialogue Play Conversation ◀── AC_Dialogue (Target)
       │
       └── Conversation: DT_YourConversation
```

**Expected result:** the conversation starts when the level begins. If you do not have a Data Table yet, continue to the [conversation guide](02-conversations.md).

### Example: Actor Component Added to the Player

![Installing the AC_Dialogue component](https://raw.githubusercontent.com/wohostudios/ue5-dialogue-system-starter-pack-es/main/images/instalacion-actor-component.png)

## Start Dialogue Through Interaction

`BeginPlay` is used only for the initial demonstration. To begin a conversation when interacting with an NPC, call `Dialogue Play Conversation` from your project's interaction event after creating the dialogue widget.

**Do not assume every template uses the same interaction input.** You may need to configure Enhanced Input and the relevant actor reference for your template.

## Template Compatibility

The Actor Component architecture does not require replacing the `GameInstance`, `GameMode`, or `PlayerController`. Add the component to the appropriate Actor in First Person, Third Person, or other templates. Adapt the conversation trigger to your project's gameplay logic.
