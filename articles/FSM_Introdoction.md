---
title: DEAL FSM Introduction  
description: An introduction to DEAL FSM
author: Kevin  
date: 2024-09-15
---

# What is a Finite State Machine?

A **Finite State Machine (FSM)** is a widely-used game design concept and a mathematical model of computation. In essence, it's an abstract machine that can be in exactly one of a finite number of states at any given time.

## Real-World Example: A Door

Consider a simple real-world example: a door. A door can be in an "opened" state or a "closed" state. The FSM helps define these states and the transitions between them.

### States:
- **Opened**: The door is fully open.
- **Closed**: The door is fully closed.

### Transition:
- **Condition**: A transition occurs based on an input, such as pressing a button or sensing motion. For instance, if a motion sensor detects someone approaching, it triggers the condition to transition from the "Closed" state to the "Opened" state. Conversely, if no motion is detected for a certain period, the door transitions back to the "Closed" state.

### Summary:
In this example, the FSM manages the door’s behavior, allowing it to switch between "Opened" and "Closed" based on specific conditions (like motion detection). Transitions dictate when and how the door moves between these states, ensuring a smooth operation based on real-world inputs.

For more details, please refer to the [Wikipedia page](https://en.wikipedia.org/wiki/Finite-state_machine).

# Basic FSM Components in DEAL

The DEAL Toolkit’s FSM is composed of four main Scriptable Objects (SO): **State Machine**, **State**, **Action**, and **Condition**. Each of these components can be fully customized to fit your game's needs.

Game designers can define any turn-based game using several states. The relationship between the components is structured as follows:  
`ScriptableStateMachine -> ScriptableState -> ScriptableCondition -> ScriptableAction`

## Scriptable StateMachine

This is the core FSM Scriptable Object (SO) that holds a list of transitions, each leading to different Scriptable States. The `ScriptableStateMachine` SO is the primary data source for the `CardStateMachineComponent` class, which executes the entire game flow.

> Create a new state machine SO by navigating project window and right-click: `Create > DealToolkit > FSM > StateMachine`.


Each transition element includes four variables:

1. **Origin State (ScriptableState SO)**: This is the current state (required).
2. **Condition (ScriptableCondition SO)**: This checks whether the transition should occur (optional).
3. **True State (ScriptableState SO)**: The state to transition to if the condition is met (optional).
4. **False State (ScriptableState SO)**: The state to transition to if the condition is not met (optional).

The Condition returns a boolean value, determining whether to transition to the next state. If the next state is not specified, the FSM will remain in the Origin State until a state change occurs.

## Scriptable State

This is the core structure representing a state within the FSM, responsible for executing every action listed in the target `ScriptableAction[]` array. 

> Create a new state SO by navigating project window and right-click: `Create > DealToolkit > FSM > State`.

Each `ScriptableState` can trigger different actions at various points:

- **OnEnterState**: Actions to be executed when entering the state.
- **OnExitState**: Actions to be executed when leaving the state.
- **OnUpdateState**: Actions to be executed during each frame while in the state.

| **State**      | OnEnterState   | OnExitState   | OnUpdateState   |
| -------------- | -------------- | ------------- | --------------- |
| **Action List** | _entryActions_ | _exitActions_ | _updateActions_ |
| **Invoke Timing** | When entering the state | When leaving the state | Every frame during the state |

## Scriptable Action

Scriptable Actions define the behaviors that should be performed in the game, such as card animations or displaying dialogs.

> Create a new action SO by navigating project window and right-click: `Create > DealToolkit > FSM > Action`.

For example, `TileDeal_1Card_PreAction` will pick one card from the tile. This action includes three variables:

| **Variable**      | Description   | 
| -------------- | -------------- |
| **Actor** | The target performer (e.g., Tile) | 
| **Actor Params** | Parameters for the Actor (e.g., Tile Number) |
| **Card Choice** | Options for card count, draw rule, and visibility (Is Revealed) |


## Scriptable Condition

Scriptable Conditions determine whether the FSM should transition from one state to another based on specific conditions.

> Create a new condition SO by navigating project window and right-click: `Create > DealToolkit > FSM > Condition`.

For example, the `WaitChangePlayer_Condition` will trigger a state transition upon receiving the `ChangePlayer` event.

| **Variable**      | Description   | 
| -------------- | -------------- |
| **Event Name** | The event that triggers the condition (e.g., ChangePlayer) | 

---
