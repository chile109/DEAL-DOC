---
title: How to extend DEAL FSM
description: This document guide you create custom action and state for your game.
author: Kevin
date: 2023-03-22
---

# How to extend DEAL FSM

![alt-text](https://res.cloudinary.com/djpxpezra/image/upload/v1679639277/superblog-image-gen_srz96t.png)

## Quick Start

To extend the custom logic of this DEAL State Machine, you can create new `ScriptableAction`, `ScriptableCondition`, and `StateTransition` SOs. For example, you might want to add a new action called `ShuffleAction` that shuffles the deck before dealing cards to players.

1. Create a new `ScriptableAction` SO called `ShuffleAction`.
2. In the inspector of the `ShuffleAction` SO, add a public method called `Execute()`.
3. Implement the logic for shuffling the deck in the `Execute()` method.
4. Create a new `StateTransition` SO called `InitialShuffleTransition`.
5. Set `99_InitialDeal_State`
6. Set its `_trueState_` to be the start state (`99_Start_State`).
7. Set its `_falseState_` to be an empty state (`99_Empty_State`) since we don't want any other behavior if shuffle fails.
8. Add a new instance of your custom condition that checks if shuffle is successful in this transition's `_condition_`.
9. Add an instance of your new `ShuffleAction` in the `_entryActions_` array of your start state (`99_Start_State`).

When your game goes from dealing to starting, it will run your custom shuffle action first. If it works, the game will move to the start state. If it doesn't work, the game will stay in the dealing state. You can make other custom actions and conditions to use in transitions between different stages of the game for more complicated game play.

### Basic

1.  `ScriptableState (SO)`: The core state structure with method executin every action listed in the target `ScriptableAction[]` array

    | **State**      | OnEnterState   | OnExitState   | OnUpdateState   |
    | -------------- | -------------- | ------------- | --------------- |
    | **ActionList** | _entryActions_ | _exitActions_ | _updateActions_ |

2.  `ScriptableAction (SO)`: Abstract SO class that can be executed
3.  `ScriptableCondition (SO)`: Abstract SO class that can verify itself and return a boolean value
4.  `StateTransition (Structure)`: Includes the `ScriptableCondition` to check for `_originState_` to make transition to `_trueState_`/`_falseState_` depending on the condition, if `_falseState_` is set to the given `_emptyState_`, this means that the transition will remain on the same state until condition is met.
5.  `ScriptableStateMachine (SO)`: The core FSM SO which can hold a list of `StateTransition`s
