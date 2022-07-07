

## Gathering requirements / exploring the domain
Go through the rules and use event storming to figure out what's going on

HandsDealt/GameStarted
- contains players
- their cards
- discard pile
- draw pile

DiscardPileRestarted

// TODO - Maybe just CardPlayed instead individual card types?
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
