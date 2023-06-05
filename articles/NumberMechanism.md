---
title: General Mechanism
description: This document define the basic mechanism of general number card games.
author: Kevin
date: 2023-06-01
---

# General Number Card Game Mechanism

Please refer to wiki for example games:

- [Texas hold 'em](https://en.wikipedia.org/wiki/Texas_hold_%27em)
- [Blackjack](https://en.wikipedia.org/wiki/Blackjack)
- [Big Two](https://en.wikipedia.org/wiki/Big_two)
- [Sevens](https://zh.wikipedia.org/zh-tw/%E6%8E%92%E4%B8%83)
- [Rummikub](https://en.wikipedia.org/wiki/Rummikub)
- [Uno](<https://en.wikipedia.org/wiki/Uno_(card_game)>)

## Card Tile

The Card Tile is an essential component of card games. It determines the available cards for dealing and gameplay. Key aspects of the Card Tile include:

- Card Pool: The total number of cards in the deck and the specific cards included.
- Dealing Order: The sequence in which cards are distributed and which player to deal next.
- Card Drawing: The number of cards can be drawn by each player during the game.

Types of Card Tile:

|                   | **Uno**         | **Texas Hold'em**    | **Rummikub**        |
| ----------------- | --------------- | -------------------- | ------------------- |
| **Pool**          | 108             | 1 Set without Jokers | 2 Sets with 2 Joker |
| **Dealing Order** | Transpose       | Fixed                | Fixed               |
| **Card Drawing**  | Single/Multiple | Single               | Single              |

## Hand Deck

The hand Deck refer to the cards held by individual players during the game. Key aspects of hand cards include:

- Cards in the Player's Hand: The number of cards each player can hold.
- Deck Sorting: The order in which cards are arranged in the hand. This can vary based on game rules.
- Poker Pattern Types:
  ![alt-text](https://res.cloudinary.com/djpxpezra/image/upload/v1685682552/PokerPatternImage_eadpoz.png)

Types of Hand Cards:

|                     | **Big Two**     | **Texas Hold'em**     | **Rummikub**    |
| ------------------- | --------------- | --------------------- | --------------- |
| **Amount**          | 13              | 2                     | 14              |
| **Deal Type**       | Pattern         | None                  | Single          |
| **Usage Scenarios** | Compare Pattern | Final hand evaluation | Sets Collection |

## Showdown Pile

The showdown pile refers to the designated area where cards are revealed and placed after the final betting round in a poker game. It is where players showcase their hands and determine the winner. Key aspects of the showdown pile include:

- Types of Piles:
  - Community Pile: A pile where the community cards, also known as the board cards, are placed.
  - Player Piles: Individual piles where each player reveals and displays their hole cards.

Types of Settlement Piles:

|                     | **BlackJack** | **Sevens**               | **Texas Hold'em**          |
| ------------------- | ------------- | ------------------------ | -------------------------- |
| **Community Pile**  | None          | Multiple (e.g., 4 suits) | 5 community cards on board |
| **Player Piles**    | Single        | Single                   | 2 hole cards per player    |
| **Usage Scenarios** | Scoring       | Link/Scoring             | Final hand evaluation      |

## Player Behavior

The player behavior refers to the actions that players can take during the game. Key aspects of player behavior include:

| Behavior | Description                                                               |
| -------- | ------------------------------------------------------------------------- |
| Draw     | Players draw cards from the Tile, Deck, or Pile..                         |
| Deal     | Place a single card or a set of pattern cards into a Tile, Deck, or Pile. |
| Discard  | Players choose to discard or abandon the cards they own.                  |
| Pass     | Players decide to give up or skip the current round.                      |

## Beting Action

For Extra Player Interaction, the game can be designed with betting actions.
Take the `Texas Hold'em` as an example, the common betting process is as follows:

| **Type** | **Timing**             | **Action Description**                                                                 |
| -------- | ---------------------- | -------------------------------------------------------------------------------------- |
| Blinds   | Before the game starts | A Player place mandatory bets called blinds.                                           |
| Check    | During a betting round | A player chooses to pass the action to the next player without placing a bet.          |
| Bet      | During a betting round | A player places chips into the pot, setting the amount for other players to match.     |
| Call     | During a betting round | A player matches the current bet to stay in the hand.                                  |
| Raise    | During a betting round | A player increases the current bet, forcing other players to match the new higher bet. |
| Fold     | During a betting round | A player discards their cards and forfeits any bets made previously.                   |
