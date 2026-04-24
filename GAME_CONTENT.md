# Fluffy Little Hamster — Game Content Reference

## Overview
Single-file browser game (Three.js r128). First-person 3D emotional life sim.
Player cares for a hamster to build trust over time. Daily interactions reset at midnight.

## Game Flow
story → setup → naming → playing

### Story Mode
- Opening: delivery box near door wobbles when player approaches
- Press [E] to open the box → hamster peeks out → caption "it's your new friend"
- Press [E] again → transitions to Setup

### Setup (Cage Decoration)
Player stands at a wooden bench and looks at + presses [E] on mini items to choose:

**Front row:**
| Category | Options |
|---|---|
| Hideout | none · wooden house · clay igloo · log tunnel |
| Food | seed mix · pellets · veggies |
| Cage colour | natural wood · dark walnut · white ash · sage wood |

**Back row:**
| Category | Options |
|---|---|
| Bedding | natural · pink · lavender |
| Water | bottle · corner sipper · water dish |
| Sand bath | none · natural sand |
| Extras | running wheel · climbing log |

Each section has a floating label. Cage stays hidden; after pressing the "done" sign → naming screen → cage + hamster revealed together.

### Naming
- Text input appears, player types hamster name (max 24 chars), presses Enter
- Default: "little one"

### Playing
All gameplay happens here. Pointer-lock FPS. ESC to pause.

---

## Controls
| Key | Action |
|---|---|
| WASD / Arrow keys | Move |
| Mouse | Look |
| E | Interact (pick up item · use item at cage · try holding hamster · buy shop item) |
| T | Open mood journal |
| Q | Whistle near cage (once/day, +1 trust) |
| ESC | Pause |
| Click | Lock mouse / enter game |
| Type "showme" | Open secret stats panel |

---

## Trust System
Hidden stat (0–100). Never shown directly — only revealed via "showme" panel.

### How trust is gained
| Action | Trust |
|---|---|
| Mood journal entry | +4 base (+1–3 extra for longer writing) |
| Treat jar | +3 |
| Bedding bag | +2 |
| Cleaning cloth | +2 |
| Music box | +2 |
| Sketchbook | +2 |
| Whistle [Q] | +1 |
| Hold (pickup) | +3 |
| Hold (trickle, every 2.5s) | +0.5 |
| Hold (completed 10s) | +1 bonus |
| Passive (over time) | +0.003/s |

### Trust stages & behaviour
| Range | Stage | Hamster behaviour |
|---|---|---|
| 0–25 | Unfamiliar | Hides often, almost never approaches, flees when player gets close to cage, 5% hold chance |
| 26–50 | Curious | Less hiding, presses against glass, cautious approaches, 30% hold chance |
| 51–75 | Comfortable | Approaches often, stays near, explores actively, 70% hold chance |
| 76–100 | Bonded | Approaches eagerly, stays near constantly, minimal hiding, 95% hold chance |

### Hold attempt (pressing [E] near cage)
- Probability depends on trust stage (see above)
- Hamster calm state (IDLE, APPROACH, STAY_NEAR, EAT, DRINK, GLASS_RUB) = full odds
- Hamster agitated (HIDE, EXPLORE, etc.) = 50% of odds
- On failure: hamster flees to HIDE, interact prompt flashes rejection message
- On success: hamster appears in player's hands for up to 10 seconds
- Press [E] to put down early, or hold full 10s for completion bonus

---

## Mood Journal
Press [T] anytime (or [E] near cage when hold already used today).

### Mood options
| ID | Label | Colour |
|---|---|---|
| happy | happy | gold |
| excited | excited | orange |
| calm | calm | blue |
| neutral | neutral | grey |
| tired | tired | purple-grey |
| nervous | nervous | yellow-green |
| anxious | anxious | tan |
| overwhelmed | overwhelmed | red-brown |
| sad | sad | blue-grey |

- First entry of day: earn +1 shop point, choose mood, optionally write up to 400 chars
- Writing more = extra trust (+1 per ~100 chars, up to +3)
- Hamster's behaviour shifts based on chosen mood for the rest of the day

### Mood history / calendar
- Access from pause menu → "mood journal", or from mood overlay → "view past entries"
- Monthly calendar grid; days with entries show the mood's colour as background
- Click a day to see full entry detail

---

## Care Items (on the wooden shelf, left side of room)
All items reset at midnight. Pick up with [E], carry to cage, press [E] to use.
Closest item within 1.4 units is selected when multiple are nearby.

| Item | Location on shelf | Trust |
|---|---|---|
| treat jar | rightmost | +3 |
| bedding bag | second from right | +2 |
| cleaning cloth | centre | +2 |
| music box | second from left | +2 |
| sketchbook | leftmost | +2 |

### Reactions when used
- **Treat jar**: Hamster goes EXPLORE, then EAT. Caption varies (e.g. "dives straight in ♡")
- **Bedding bag**: Hamster goes BURROW, then IDLE. Caption (e.g. "burrowing immediately ♡")
- **Cleaning cloth**: Hamster hides then EXPLORE. Caption (e.g. "sparkling clean ♡")
- **Music box**: Hamster GLASS_RUB/approaches. Caption (e.g. "tilting their head ♡")
- **Sketchbook**: Hamster approaches, presses nose to glass. Caption (e.g. "sniffed the page ♡")

---

## Hamster AI Behaviours
State machine; re-evaluates when duration expires.

| Behaviour | Description |
|---|---|
| IDLE | Grooming — sits still, front paws raised, head bobs |
| EXPLORE | Walks to a random point, sniffs around on arrival |
| HIDE | Runs to hideout entrance, slides inside and shrinks to near-invisible |
| GLASS_RUB | Walks to tank wall, presses nose and rubs |
| BURROW | Digs in bedding — body bobs, head animates |
| INTERACT | Walks to an accessory and sniffs it |
| APPROACH | Walks toward player's position on the glass |
| STAY_NEAR | Sits up tall, watches player, head tracks |
| USE_WHEEL | Runs on wheel (if present) |
| EAT | Visits food bowl, head bobbing |
| DRINK | Visits water container |
| SAND_BATH | Rolls and shakes in sand bath |
| CLIMB | Climbs on branch/log (if present) |

Behaviour scores are weighted by trust + mood bias + randomness + per-stage caps.

---

## Hamster Avoidance (low trust)
At trust < 26: when player camera comes within 2.8 units of cage centre, hamster triggers HIDE and flees to the far side of the cage.

---

## Daily Shop
Three pedestals near the front of the room. Stock rotates daily (seeded by date).
Points are earned from mood journal entries. Shop shown after setup complete.

### Shop item pool (all items, each ~2–5 pts)
wooden bridge · gem stone · cloud bed · cozy den · bell · flower pot · branch log · sand bath · food bowl (upgrade) · water bottle (upgrade) · small house · ceramic igloo · etc.
(~20+ items total — 3 shown per day, rotate daily)

### Glow colours
- Green glow: 2 pts
- Gold glow: 3–4 pts
- Orange glow: 5 pts

---

## Cage Accessories (from setup or shop)
| Accessory | Effect on AI |
|---|---|
| Running wheel | Enables USE_WHEEL behaviour |
| Food bowl | Enables EAT behaviour |
| Water container | Enables DRINK behaviour |
| Sand bath | Enables SAND_BATH behaviour |
| Branch/log | Enables CLIMB behaviour |
| Hideout | HIDE behaviour targets it; hamster enters properly |

---

## Hideout Behaviour (entering)
When hamster does HIDE with a hideout present:
1. Walks to entry point just outside the door (entryDZ/entryDX offset)
2. Slides to hideout centre + shrinks scale to ~0.12 (looks like ducking inside)
3. Scale restores when leaving HIDE

---

## Secret Panel ("showme")
Type "showme" anywhere while in game → opens overlay showing:
- Trust score (exact number)
- Hamster personality traits (generated from name seed)
- Your care history stats

---

## Profile System
Up to multiple profiles. Each profile stores:
- Owner name, hamster name
- Setup choices (bedding, hideout, food, water, sand, wheel, branch, cage colour)
- Trust score, daily care used, mood history, shop points, bought items

---

## Pause Menu
- Continue (re-locks mouse)
- Mood journal
- Guide (full how-to-play reference)
- How to play (tutorial overlay)
- Switch profile

---

## Tutorial Overlay (first play only)
5 steps shown on first play, stored in localStorage so it only appears once.
Accessible again from pause menu → "how to play".

Steps: welcome · [E] and [T] keys · care items · daily shop · take your time
