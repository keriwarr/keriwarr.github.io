---
layout: post
title:  "Notes: Running a Prediction Market Games Night"
date:   2023-08-14
---

# Notes: Running a Prediction Market Games Night

status: rough draft, unedited.

## Prior Art

- https://shakeddown.wordpress.com/2022/08/04/what-i-learned-about-running-a-betting-market-game-night-contest/

## Structure

I like to think of this event as a nerdy twist on a standard trivia night. Participants "submit" their answers not by filling out an answer sheet, but by betting in a prediction market. This format admits for many interesting and fun categories of questions other than standard trivia:
- questions about what will be true of the event/venue/attendees at some specific time later that day, e.g.:
  - "how many people will be sitting at this table at 7:30pm?"
  - "who will win this real-time in-person blitz chess game?"
- estimation questions, e.g. "how many paperclips are in this jar?"
- meta questions, e.g.:
  - "how many questions will I ask tonight?"
  - "will any question have a 'total volume' >M$X by the time it closes?"
- random fun things such as distributing tokens to everyone and asking "who will have the most tokens at X time?"
- which of these poems was written by an LLM?
- actual trivia questions (multiple choice)

One thing all these questions have in common is that the answer is knowable by the end of the event.

I think ~2 hours is about right for this event. ~15 minutes for learning how to use manifold markets and how the event will run. ~90 minutes for ~20 questions. ~15 mintues for resolving questions, discussion, etc.

### Rules

- You can use google for anything that doesn't have a definite, googlable answer

### First Mover Advantage

The first person to bet on a market has an opportunity to "correct" the market more than anyone who follows, and therefore, has an advantage. Possible approaches:
- Free for all - whomever gets to the market first gets to bet first. This is dissatisfying - it privileges folks with fast reaction times, fast internet, etc. - not fun
- Initialize the market closer to the true value - gives away the game!
- My personal preference: for the first N seconds after opening a new market, one designated person (the "First Mover") is the only person who may bet on the market. After a timer expires, the market is generally available and anyone may bet. This relies on the honor system.
  - It seems somewhat complex but in my experience people "get it" pretty quickly.
  - Select the first mover by round-robin.

## Logistics

1. Make a private group on https://manifold.markets
   - this will prevent automated market making bots from participating in you event!
1. Create a group chat for the event. You will use this to share market links with participants
1. Share an invite link to the manifold group in the group chat
1. The manifold markets mobile app works better than desktop browser for this event - recommend participants to bring a phone and install the app
1. When you create a manifold markets account you automatically get 500 Mana. This is the budget for the game. If someone already has an account, ask them to spend no more than M500 (tricky to do in practice). If they don't have M500... send them some mana?
1. Demonstrate how to use manifold.markets!
   - gotcha: if you buy and then immediately sell in a market, you actually lose a small amount of mana. I think this is a somewhat helpful intuition pump for understanding manifold.

## Notes

- Avoid numeric markets. Instead, make bucketed multiple choice markets
- I recommend creating one initial market that will be resolved N/A in which participants can buy YES/NO, and get experience using the UI and navigating in the app
  - double check whether losses due to buying then selling are still reversed upon N/A resolution before doing this
- I recommend creating one or two warm-up questions, to make sure everyone understands how the game works before they turn their attention to winning e.g.:
  - "When I roll this six sided die, will it come up with a 4?"
  - and/or some question that is certainly true/false. Introduces the notion of diminishing marginal returns and taking free money
- Get a good night's sleep before running this event. Make sure that you have fun too!
- You may consider having one or two breaks during the question ask so folks can revisit older questions, and so you can resolve some questions to free up capital.
- Make sure to leave some time at the end for folks to negotiate, discuss, and hang out
- Close questions before declaring the answer!
- Write down your question and answer schedule in advance
- Index the question titles
- Consider using a timer to stay on schedule
- Resolving "meta" type questions can be a real PITA

### Other fun question ideas

- "which option will have the highest %?", then make some silly options like ("schelling point" and "$420.69")
- "who will be in first (or second?) place on the group leaderboard at X:00 PM?" (post this one near the beginning of the night)

## Friction

- Manifold can be a little laggy sometimes. This introduces some unfortunate but unavoidable unfairness.
- A fun idea that I had for a question was "Who will directly send me the most mana?", however new accounts cannot send mana
- You can not currently sort group markets in the order in which they were created
- The leaderboard refreshed every ~15 minutes, so you won't be able to conclusively declare the winner until up to 15 minutes after the last market has been closed

## Misc.

one could make running this event quite a bit less difficult with a bespoke web ui that hits the manifold api

questions, thoughts, etc. => keri@warr.ca
