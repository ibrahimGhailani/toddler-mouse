# Survival Mode Rules

## Objective
Keep the health timer alive as long as possible by clicking circles before they disappear.

## Health Timer
- Starts at **10 seconds**
- Drains continuously in real time
- **Game over** when it reaches zero
- Caps at **15 seconds** (cannot exceed this)

## Scoring Time Back
Each circle you click adds time back to the health timer. The faster you click after the circle appears, the more time you earn:

| Reaction time | Time added |
|---------------|------------|
| Under 0.5s | +3.0s |
| 0.5s – 3.0s | +0.5s to +3.0s (linear) |
| Over 3.0s | +0.5s |

Missing a circle (letting it disappear) adds no time.

## Waves
A new wave begins every **30 seconds**. Between waves, all circles clear and a brief "Wave X" banner appears — the health timer pauses during this transition.

Each wave is harder than the last:

| Wave | Max circles on screen | Circle size | Circle lifetime |
|------|-----------------------|-------------|-----------------|
| 1 | 1 | 20% | 5.0s |
| 2 | 1 | 18% | 4.5s |
| 3 | 2 | 16% | 4.0s |
| 4 | 2 | 14% | 3.5s |
| 5 | 3 | 12% | 3.0s |
| 6 | 3 | 10% | 2.5s |
| 7 | 3 | 9% | 2.0s |
| 8+ | 3 | 8% | 1.5s |

Circle size is expressed as a percentage of the shorter screen dimension.

## Score
Your score is the total number of circles popped. The game over screen shows your score and the wave you reached.
