---
title: Common Usage FSM SO
description: This document show the FSM SO common usage
author: Kevin
date: 2023-03-22
---

# Common Usage

The Card State Machine is a system that manages the actions ScriptableObject taken during a card game.

A `ScriptableStateMachine` consists of a list of `ScriptableState` and `StateTransition` SOs. Each `ScriptableState` contains a list of `ScriptableAction` SOs that are executed when the state is entered, exited, or updated. Each `StateTransition` contains a `ScriptableCondition` SO that checks if the transition should be made from the origin state to the true state or false state.

## Default Action Types

- `ChangePlayerAction`: Rotate to the player specified by `ActionActor` enum and params
- `DealAction`, `DrawAction`: Deal means actor will give out card to target, Draw means actor will pick card from target.
- `TrasnsferAction`: Similar to Deal/Draw, but for transferring chips.
- `PreAction`, `PostAction`: During PreAction, the action will acquire the involved decks and players, then request `CardStateMachineComponent` to WaitTurnLock until the actor has made a valid `CardChoice`, which will then be executed by PostAction.
- `CardChoice`: Serializable structure that can be set to request the state machine to host a **Card Pick**.
  - `count`: How many cards should be picked
  - `rule`: Enum CardChoiceRule that records the pick rules (like *FromTop*, *Random*, *Specific*)
  - `isRevealedToPicker`: Should the picker see the cards when picking?
- `EliminatePlayerAction`: Eliminate the player from the game
- `ModifyPlayerPropertyAction`: Modify the target player's property with reference player's property
- `UpdatePlayerPropertyAction`: Update the target player's property with the given value
- `ShowDialogAction`: Pop up a dialog to selected players
- `UpdateStateEventAction`: Update the state machine's state

## Default Condition Types

- `EndOfTurnCondition`: check if state is locked by WaitTurnLock
- `EndOfSystemLockCondition`: check if state is locked by WaitSystemLock
- `AlwaysTrueCondition`: always passes, used for transition phase
- `CheckDeckCountCondition`: checks if given actor has given amount of cards, normally used in intial deal
  - Example usage: Checks if all players have 5 cards, so that the game can start, else continue dealing cards to players
- `CheckDefeatedCondition`: checks if the specific player has been defeated
- `CheckGameOverCondition`: set the amount of `maxEliminatedPlayerCount`, if the amount of eliminated players is equal to or greater than `maxEliminatedPlayerCount`, the game is over
- `CheckPlayerPropertyCondition`: check target player's property against the given value `rawPropertyValue`
- `ComparePlayerPropertyCondition`: compare the target player's property with the reference player's property
- `CompareScoreCondition`: compare the subject player's card score with the control player's card score
  - `XXXCheckScale`: check only the cards from player's buffer, or check the whole deck
    - Buffer: When player selects one or many cards from their deck, but hasn't perform any actual transfer yet (for example: about to deal), these cards are temporarily placed in the buffer
  - `XXXCounter`: method to count the scores
    - `SumNumber`: sum all the card numbers
    - `Max`: find the max number
    - `Min`: find the min number
    - `MostOccuredNumber`: find the most occurred number
    - `Average`: calculate the average number
    - `Mid`: find the middle number
    - `GivenMinusSumNumber`: given score (stored in `CounterParams`) minus the sum of all cards
    - `PokerEval`: evaluate the poker hand using external `PHEval` library
    - `BaccarateRangeSum`: sum the card numbers using Baccarate rules
- `MatchScoreMultipleCondition`: check subject player's card score against a group set of rules
  - Example usage: Check if the player's score is larger than 3 and smaller than 6
- `WaitEventCondition`: wait until a state event is triggered locally
- `WaitForGroupEventCondition`: wait until a state event is triggered for all members in selected group

## Extend usage

If you feel like customizing the action or condition, you can create your own `ScriptableAction` or `ScriptableCondition` SOs. Check out the `ExtendFSM` article for more information.
