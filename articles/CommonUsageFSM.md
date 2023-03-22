---
title: Common Usage FSM SO
description: This document show the FSM SO common usage for game 99
author: Kevin
date: 2023-03-22
---

# Common Usage

The Card State Machine is a system that manages the actions ScriptableObject taken during a card game.
Here show the usage of pre-defined FSM SO in example game 99.

## Action

- `ChangePlayerAction`: Rotate to the player specified by `ActionActor` enum and params
- `DealAction`, `DrawAction`: Deal means actor will give out card to target, Draw means actor will pick card from target.
- `PreAction`, `PostAction`: During PreAction, the action will acquire the involved decks and players, then request `CardStateMachineComponent` to WaitTurnLock until the actor has made a valid `CardChoice`, which will then be executed by PostAction.
- `CardChoice`: Serializable structure that can be set to request the state machine to host a **Card Pick**.
  - `count`: How many cards should be picked
  - `rule`: Enum CardChoiceRule that records the pick rules (like *FromTop*, *Random*, *Specific*)
  - `isRevealedToPicker`: Should the picker see the cards when picking?

## Condition

- `EndOfTurnCondition` : check if state is locked by WaitTurnLock
- `AlwaysTrueCondition` : always passes, used for transition phase
- `CheckDeckCountCondition` : checks if given actor has given amount of cards, normally used in intial deal
  - Example : `99_CheckAllPlayer5Cards_Condition` Checks if all players have 5 cards, so that the game can start

## State

- `99_Inital_State` : Initial state that will check if players all have 5 cards. If true -> start state, else -> initial deal state
- `99_InitialDeal_State` : The initial state to deal 1 single card per entry to the current player
- `99_Empty_State` : Used for empty state behaviour
- `99_Start_State` : The beginning of player turns
- `99_PlayerDraw_State` : Player draws a card from tile
- `99_PlayerTurn_State` : Player's turn to pick a card to deal to the counting deck
- `99_Validation_State` : Verify if this game is over based on whether next player can make any moves, should transition to GameOver State and calculate the winner/loser
