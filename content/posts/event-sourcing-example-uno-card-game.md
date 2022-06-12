

## Gathering requirements / exploring the domain
Go through the rules and use event storming to figure out what's going on

DeckShuffled
HandsDealt
DiscardPileStarted
WildFourReturnedToDeck
DeckShuffled
DiscardPileStarted

// Discard pile depleeted
DiscardPileShuffled
DiscardPileStarted

NumberCardPlayed
PlayerDrewACard
ReverseCardPlayed
SkipCardPlayed
DrawTwoCardPlayed
PlayerDrewTwoCards
WildCardPlayed
WildDrawFourCardPlayed
WildFourChallenged
WildFourChallengeSucceeded
WildFourChallengeFailed
PlayerDrewFourCards

UnoDeclared
UnoDeclarePenaltyRaised

GameCanceled
PlayerWon

// Maybe
PlayerFolded
PlayerKicked

Next: 
User interface
How are users going to interact with the system

Then using event modeling map read models events actions etc...

Then code
