---
title: Poker Mechanism
description: This document define the basic mechanism of poker games.
author: Kevin
date: 2023-06-01
---

# Poker Mechanism

Common Game Rules [Link to PokerStars Rules](https://www.pokerstars.com/en/poker/games/rules/)

### Card Deck

The card deck is an essential component of card games. It determines the available cards for dealing and gameplay. Key aspects of the card deck include:

- Card Pool: The total number of cards in the deck and the specific cards included.
- Dealing Order: The sequence in which cards are distributed and which player to deal next.
- Shuffling Feature: Whether the deck is shuffled before each round or remains static.

Types of Card Decks:

|                     | **Big Two** | **Texas Hold'em** | **Mahjong** |
| ------------------- | ----------- | ----------------- | ----------- |
| **Flow**            | None        | Output            | Output      |
| **Card Drawing**    | None        | Single            | Single      |
| **Usage Scenarios** | No Deck     | Single Deck       | Array Deck  |

### Hand Cards

The hand cards refer to the cards held by individual players during the game. Key aspects of hand cards include:

- Cards in the Player's Hand: The number of cards each player can hold.
- Deck Sorting: The order in which cards are arranged in the hand. This can vary based on game rules.
- Player Actions: Various actions players can take with their hand cards, such as dealing, forming combos, identifying patterns, passing, discarding, and placing bets.

Types of Hand Cards:

|                     | **Big Two** | **Texas Hold'em** | **Mahjong** |
| ------------------- | ----------- | ----------------- | ----------- |
| Amount              | 13          | 2                 | 16          |
| Deal Type           | Pattern     | None              | Single      |
| **Usage Scenarios** | Compare     | Compare           | Collection  |

- Poker Pattern Types:
  ![alt-text](https://asset.cloudinary.com/djpxpezra/6495e28a0ffc888e719da203a4982eb9)

### Settlement Pile

The settlement pile refers to the location where cards are placed after use or when they are no longer in play. Key aspects of the settlement pile include:

- Types of Piles:
  - Shared Pile: A pile shared among all players, usually used for as a discard pile.
  - Personal Pile: A pile dedicated to each player for scoring, where cards are placed based on individual gameplay rules.

Types of Settlement Piles:

|                     | **BlackJack** | **Sevens**                 | **Mahjong**            |
| ------------------- | ------------- | -------------------------- | ---------------------- |
| **Shared Pile**     | None          | Multiple (4 suits)         | Single                 |
| **Personal Pile**   | Single        | Single                     | Multiple               |
| **Usage Scenarios** | Scoring       | 4 Suit Pile / Discard Pile | Public Pile/Score Pile |
