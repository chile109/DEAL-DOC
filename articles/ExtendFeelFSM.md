---
title: How to extend Feel FSM
description: This document guide you create custom action and state for your game.
author: Kevin
date: 2023-03-22
---

# How to extend Feel FSM

## Quick Start

To extend the custom logic of this UCE State Machine, you can create new `ScriptableAction`, `ScriptableCondition`, and `StateTransition` SOs. For example, you might want to add a new action called `ShuffleAction` that shuffles the deck before dealing cards to players.

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

### Common Usage

The Card State Machine is a system that manages the actions taken during a card game. It includes several actions, such as the Change Player Action, which rotates to the player specified by the ActionActor enum and parameters.

#### Action

- `ChangePlayerAction`: Rotate to the player specified by `ActionActor` enum and params
- `DealAction`, `DrawAction`: Deal means actor will give out card to target, Draw means actor will pick card from target.
- `PreAction`, `PostAction`: During PreAction, the action will acquire the involved decks and players, then request `CardStateMachineComponent` to WaitTurnLock until the actor has made a valid `CardChoice`, which will then be executed by PostAction.

#### CardChoice

Serializable structure that can be set to request the state machine to host a **Card Pick**.

- `count`: How many cards should be picked
- `rule`: Enum CardChoiceRule that records the pick rules (like *FromTop*, *Random*, *Specific*)
- `isRevealedToPicker`: Should the picker see the cards when picking?

#### `Condition`

- `EndOfTurnCondition` : check if state is locked by WaitTurnLock
- `AlwaysTrueCondition` : always passes, used for transition phase
- `CheckDeckCountCondition` : checks if given actor has given amount of cards, normally used in intial deal
  - Example : `99_CheckAllPlayer5Cards_Condition` Checks if all players have 5 cards, so that the game can start

#### `State`

- 99:
  - `99_Inital_State` : Initial state that will check if players all have 5 cards. If true -> start state, else -> initial deal state
  - `99_InitialDeal_State` : The initial state to deal 1 single card per entry to the current player
  - `99_Empty_State` : Used for empty state behaviour
  - `99_Start_State` : The beginning of player turns
  - `99_PlayerDraw_State` : Player draws a card from tile
  - `99_PlayerTurn_State` : Player's turn to pick a card to deal to the counting deck
  - `99_Validation_State` : Verify if this game is over based on whether next player can make any moves, should transition to GameOver State and calculate the winner/loser
