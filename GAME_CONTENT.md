# Fluffy Little Hamster — Complete Game Content Reference

---

## Story / Intro Narrative

Shown sequentially when a new player starts:

| Phase | Caption Text |
|-------|-------------|
| 0 | "a knock at the door." |
| 0 → 1 | "[E] open it" (prompt on the delivery box) |
| 2 | "oh." |
| 3 | "it's your hamster · press [E] to set up their home" |

After story: skips setup, applies defaults, goes straight to naming screen.

---

## Hamster Appearance

### Colors (9 options)

| Name | Body Hex | Belly Hex | Ear Hex | Eye Hex | Nose Hex |
|------|----------|-----------|---------|---------|----------|
| golden | #c4823a | #f0d8b0 | #f0a898 | #0e0808 | #e08898 |
| white | #f0ecea | #fcf8f4 | #f4b8b0 | #cc4444 | #f09898 |
| grey | #9898a8 | #d8d8e4 | #f0a898 | #0e0808 | #e08898 |
| cinnamon | #c05828 | #ecc090 | #f0a090 | #0e0808 | #e08898 |
| black | #2e2a28 | #706860 | #d09090 | #1a1818 | #e08898 |
| cream | #e0c898 | #f8ecd8 | #f0a898 | #0e0808 | #e08898 |
| chocolate | #7a4828 | #c89068 | #e0a090 | #0e0808 | #e08898 |
| lilac | #b0a8c0 | #e4e0ec | #f0b0c0 | #0e0808 | #e08898 |
| caramel | #d09050 | #f0dcb0 | #f0a898 | #0e0808 | #e08898 |

### Patterns (4 options)

| Name | Description |
|------|-------------|
| solid | single color all over |
| piebald | white patches on body |
| banded | lighter mid-band across belly |
| spotted | small white spots on back |

### Sizes (3 options)

| Name | Scale Multiplier |
|------|-----------------|
| petite | 0.80× |
| medium | 1.00× |
| chonky | 1.20× |

Total possible hamster appearances: 9 colors × 4 patterns × 3 sizes = **108 combinations**

---

## Cage Setup

### Bedding Themes (6 options)

| Name | Base Color | Chip Colors |
|------|-----------|-------------|
| natural | #c8a878 | #d4b896, #c8a87c, #dec8a8, #b89870, #e8d4b8 |
| pink | #d4909a | #e0a8b0, #d49098, #ecc0c8, #c88090, #f0ccd4 |
| lavender | #a8a0c0 | #b8b0d0, #a8a0bc, #d0c8e4, #9890a8, #e0d8f0 |
| sage | #98a890 | #a8b8a0, #90a888, #bcd0b4, #889880, #d0e0c8 |
| cream | #e0d8c8 | #e8e0d0, #ddd4c0, #f0e8d8, #d0c8b4, #f8f0e4 |
| lilac | #c0a8c8 | #d0b8d8, #b8a0c0, #e0c8e8, #a890b0, #f0d8f8 |

### Hideouts (4 options)

| ID | Label | Description |
|----|-------|-------------|
| null | none | no hideout |
| house | wooden house | small wooden hut |
| igloo | clay igloo | rounded clay dome |
| logtunnel | log tunnel | hollowed log |

### Food Bowl (3 options)

| ID | Label |
|----|-------|
| seed | seed mix |
| pellet | pellets |
| veggie | veggies |

### Water (3 options)

| ID | Label |
|----|-------|
| bottle | water bottle |
| corner | corner sipper |
| dish | water dish |

### Sand Bath (4 options)

| ID | Label |
|----|-------|
| null | none |
| natural | natural sand |
| pink | rose sand |
| blue | mineral sand |

### Extras (toggle on/off)

| Item | Default |
|------|---------|
| running wheel | on |
| climbing branch / log | off |

**Default cage config (applied automatically):** natural bedding · wooden house · seed mix · water bottle · wheel on · no branch · no sand bath

---

## Mood System

### Mood Options (9)

| ID | Label | Subtitle | Color |
|----|-------|----------|-------|
| happy | happy | something good is happening | #d4b060 |
| excited | excited | full of energy | #c87840 |
| calm | calm | peaceful and settled | #88b8d0 |
| neutral | neutral | just getting through it | #b0a898 |
| tired | tired | running on empty | #9898a8 |
| nervous | nervous | a little on edge | #a8b870 |
| anxious | anxious | wound up tight | #b89858 |
| overwhelmed | overwhelmed | too much at once | #c87070 |
| sad | sad | carrying something heavy | #8890b8 |

### Mood → Behavior Bias Table

Each mood adds/subtracts from behavior scoring weights for that day:

| Mood | Behavior Adjustments |
|------|---------------------|
| neutral | no changes |
| calm | idle +8, explore +3, hide −5 |
| happy | explore +10, approach +6, stay_near +4, idle −4 |
| tired | idle +15, burrow +8, explore −8, approach −6 |
| anxious | hide +15, burrow +10, glass_rub +8, approach −10, stay_near −8 |
| overwhelmed | hide +20, burrow +15, idle +8, approach −15, explore −10 |
| nervous | hide +10, glass_rub +6, approach −8, idle +5 |
| excited | explore +12, glass_rub +8, interact +8, approach +4, idle −8 |
| sad | idle +10, burrow +8, hide +5, approach −5 |

---

## Hamster AI Behaviors

### Behavior List

| ID | Name | Description |
|----|------|-------------|
| IDLE | idle | grooming, settling, staying still |
| EXPLORE | explore | walking and sniffing around cage |
| GLASS_RUB | glass_rub | pressing against cage glass |
| APPROACH | approach | moving toward player |
| STAY_NEAR | stay_near | sitting and watching the player |
| HIDE | hide | running to hideout or corner |
| INTERACT | interact | active movement in center area |
| BURROW | burrow | digging into bedding |
| USE_WHEEL | use_wheel | running on the wheel |
| EAT | eat | eating from food bowl |
| DRINK | drink | drinking from water source |
| SAND_BATH | sand_bath | rolling in sand bath |
| CLIMB | climb | climbing branch/log |

### Behavior Scoring Formula

```
score = baseWeight + trustModifier + moodBias + randomness + memoryBias
```

The hamster picks the highest-scoring behavior with some weighted randomness. It avoids repeating the same location or behavior consecutively, includes pause/hesitation micro-delays, and remembers recently visited zones.

---

## Trust System

### Trust Gain Sources

| Source | Trust Gained | Notes |
|--------|-------------|-------|
| Mood check-in (base) | +4 | once per day |
| Mood check-in (note > 10 chars) | +2 bonus | same submission |
| Mood check-in (checked in yesterday too) | +1 bonus | streak bonus |
| Give treats | +3 | once per day |
| Change bedding | +2 | once per day |
| Wipe cage | +2 | once per day |
| Play music box | +2 | once per day |
| Show sketchbook | +2 | once per day |
| Whistle [Q] near cage | +1 | once per day |
| Hold hamster | +4 | once per day, trust ≥ 35 required |
| Passive (3 min of active play) | +1 | repeating |

Maximum from one mood check-in: **+7**

### Trust Stages (0–100)

| Stage | Range | Hamster Behavior |
|-------|-------|-----------------|
| 1 — Unfamiliar | 0–25 | cautious movement, avoids player, high alert idle |
| 2 — Curious | 26–50 | observes player more, occasional approach, less avoidance |
| 3 — Comfortable | 51–75 | shares space consistently, approaches voluntarily, less hesitation |
| 4 — Trusting Companion | 76–100 | frequent proximity, stable calm behavior, occasional following |

Hold interaction unlocks at: **trust ≥ 35**

Trust is never shown directly to the player — except via the secret panel.

---

## Care & Bonding Items

Five physical items placed around the room. Pick up with [E], carry to cage, press [E] again to use. Each resets at midnight.

| ID | Display Label | World Position | Trust Gain | Cage Prompt | Hamster Reaction |
|----|--------------|---------------|------------|-------------|-----------------|
| treats | treat jar | near cage wall (left) | +3 | "give treats to [name]" | EAT behavior |
| bedding | bedding bag | near back-left wall | +2 | "change the bedding" | BURROW → IDLE |
| cleaner | cleaning cloth | near cage front floor | +2 | "wipe the cage" | HIDE → EXPLORE |
| musicbox | music box | left-center floor | +2 | "play music for them" | IDLE → STAY_NEAR |
| sketch | sketchbook | far left wall | +2 | "show drawing to [name]" | APPROACH → STAY_NEAR |

### Particle Effects Per Item

| Item | Particle Color |
|------|---------------|
| treats | warm orange/gold |
| bedding | soft beige/tan |
| cleaner | cool blue/white flash |
| musicbox | soft purple (#d4c0f0) |
| sketch | warm yellow (#f0d890) |

### Care Captions (random pick from each set)

**Treats:**
- "[name] ran right over ♡"
- "little cheeks are filling up ♡"
- "[name] loves treats ♡"
- "nibble nibble nibble ♡"
- "those tiny paws are grabbing everything ♡"
- "[name] is so happy right now ♡"

**Bedding:**
- "[name] is already digging in ♡"
- "fresh bedding, happy hamster ♡"
- "[name] loves a clean nest ♡"
- "burrowing immediately ♡"
- "cozy and content ♡"
- "[name] is fluffing it all up ♡"

**Cleaning Cloth:**
- "[name] watched you the whole time ♡"
- "sparkling clean ♡"
- "[name] sniffed every corner after ♡"
- "they noticed, they always notice ♡"
- "a clean home is a happy home ♡"
- "[name] came back out once it smelled right ♡"

**Music Box:**
- "[name] went very still ♡"
- "tiny ears perked right up ♡"
- "[name] loves this song ♡"
- "they listened to every note ♡"
- "soft music, soft hamster ♡"
- "[name] closed their eyes ♡"

**Sketchbook:**
- "[name] sniffed the page ♡"
- "you drew them something beautiful ♡"
- "[name] pressed their nose against the glass ♡"
- "they came right over to look ♡"
- "[name] seemed impressed ♡"
- "a little art, just for them ♡"

**Holding:**
- "[name] settled right into your hands ♡"
- "so small, so warm ♡"
- "[name] trusts you ♡"
- "tiny heartbeat ♡"
- "they didn't want to leave ♡"
- "[name] closed their eyes for a moment ♡"

---

## Whistle Interaction

Press **[Q]** when standing within ~3.5 units of the cage. Available once per day.

- Trust gain: **+1**
- Hamster briefly does APPROACH then returns to IDLE
- Soft gold particles spawn above cage
- Already-used message: *"you already sang to them today ♡"*

**Whistle Captions (random pick):**
- "[name] looked right at you ♡"
- "♩ they heard your little song ♡"
- "[name] perked up their ears ♡"
- "a soft melody just for them ♡"
- "[name] came closer to listen ♡"
- "♩ they always recognize your voice ♡"

---

## Daily Shop System

3 items rotate daily (seeded by date + profile ID — same day always shows the same 3 items). Items float and rotate on pedestals near the front of the room. Earn points by journaling.

### Pedestal Positions (world space)

| Slot | X | Z |
|------|---|---|
| Left | −1.4 | 4.2 |
| Centre | 0 | 4.2 |
| Right | +1.4 | 4.2 |

### Price Color Hints (glow on pedestal)

| Price | Glow Color |
|-------|-----------|
| 2 pts | soft green |
| 3–4 pts | golden yellow |
| 5 pts | warm orange |

### Points Economy

| Action | Points Earned |
|--------|--------------|
| Submit mood journal entry | +1 pt |
| Care items / holding / whistle | 0 pts (trust only) |
| Starting points | 0 |

### Shop Item Pool (12 items, 3 shown per day)

| ID | Label | Price | Shape Description |
|----|-------|-------|-----------------|
| succulent | tiny succulent | 2 pts | small pot with round green top |
| sparkle_ball | sparkle ball | 2 pts | gold glowing sphere |
| pinwheel | mini pinwheel | 3 pts | 4-blade colored pinwheel on a stick |
| tunnel | colorful tunnel | 3 pts | red half-cylinder arch |
| mirror | little mirror | 3 pts | gold torus frame with reflective disc |
| bell | little bell | 3 pts | gold bell with clapper |
| gem_stone | crystal gem | 3 pts | translucent octahedron |
| ladder | wooden ladder | 4 pts | two rails with 5 rungs |
| bridge | tiny bridge | 4 pts | curved wooden plank bridge |
| flower_pot | flower pot | 4 pts | terracotta pot with 3 flowers |
| cloud_bed | cloud bed | 4 pts | white pillow base with cloud puffs |
| cozy_den | cozy den | 5 pts | dome hideout with arched doorway |

Bought items placed permanently in cage across up to **6 decoration spots**. Daily shop refreshes at midnight.

### Buy Captions (random pick)

- "[name] is already inspecting it ♡"
- "new thing in the cage ♡"
- "[name] sniffed it immediately ♡"
- "a little upgrade ♡"
- "[name] seems pleased ♡"

---

## Secret Panel — "showme"

Type the word **showme** at any time during gameplay (not in a text input) to open the hidden stats panel. Pointer lock releases and the panel fades in.

### What It Reveals

**Trust bar** — exact trust value (0–100) with a fill bar.

**5 Personality Traits** — each shown as a dot on a sliding track between two extremes. Seeded from the hamster's profile ID so they're unique and consistent per hamster. Never change after generation.

| Left (low) | Right (high) |
|------------|-------------|
| shy | bold |
| cautious | curious |
| independent | social |
| calm | playful |
| stable | sensitive |

**History Stats:**
- Days journaled (count of unique mood entries)
- Most common mood logged
- Date of first ever entry
- Total care actions used (all-time)
- Items in cage (X / 12)

Panel title: *"things only you know"*
Hint text: *"type 'showme' anytime to open this"*
Close button returns pointer lock if in game.

---

## UI Text Reference

### Start / Enter Screen
- Title: **"fluffy little hamster"**
- Subtitle: *"click anywhere to enter your room"*

### Pause Menu (ESC)
- Header: "paused"
- Button: "continue"
- Button: "mood journal"
- Button: "switch profile"

### Mood Overlay
- Title: "how are you feeling today?"
- Subtitle: "your hamster picks up on your energy"
- Journal label: "anything on your mind?"
- Journal placeholder: *"write about your day, what happened, how you're really feeling... (optional)"*
- Character limit: 400
- Submit button: "tell them →"
- History link: "view past entries →"
- Already checked-in message: "[name] already knows how you feel today ♡"
- Confirmed message (with note): "they heard you ♡"
- Confirmed message (no note): "they understand ♡"

### Owner Name Screen (first ever launch)
- Title: "fluffy little hamster"
- Label: "what's your name?"
- Input placeholder: *"your name..."*
- Button: "meet your hamster →"
- Hint: *"press Enter or click the button"*

### Profile / Hamster Select Screen
- Title: "whose hamster?"
- New profile button: "new hamster"
- Delete confirm label: "type [hamster name] to delete"
- Delete confirm button: "delete"
- Keep button: "keep"

### History / Calendar Overlay
- Title: "mood journal"
- Weekday headers: su · mo · tu · we · th · fr · sa
- Close button: "✕ close"
- Empty note text: "no note for this day"
- Days colored by mood using each mood's hex color

### Naming Screen
- Label: "give them a name"
- Placeholder: *"little one..."*
- Default name if left blank: **"little one"**

### Points Display (top-right, visible during play)
- Format: `● N pts`
- Green dot indicator
- Fades in when entering playing state

### Held Item Bar (bottom-right, visible when carrying)
- Format: `● holding [item label]`
- Amber dot indicator

### In-World Prompts

| Situation | Prompt Text |
|-----------|------------|
| Near delivery box (story) | "[E] open it" |
| Near care item on floor | "[E] pick up [item label]" |
| Holding item, near cage | "[E] give treats to [name]" / "[E] change the bedding" / "[E] wipe the cage" / "[E] play music for them" / "[E] show drawing to [name]" |
| Near cage, trust ≥ 35, calm hamster, not held today | "[E] gently hold [name] · talk to them" |
| Near cage, other | "[name]'s home · [E] talk to them" |
| Near shop pedestal, can afford | "[E] add [item] to cage · N pts" |
| Near shop pedestal, can't afford | "[item] · N pts (need X more)" |
| Near shop pedestal, already bought | "[item] · already in the cage" |

---

## Keyboard Controls

| Key | Action |
|-----|--------|
| W A S D | move |
| Mouse | look around |
| E | interact (pick up item / use item / hold hamster / open mood / buy shop item) |
| Q | whistle near cage (once per day, +1 trust) |
| ESC | pause / unlock mouse |
| Click | lock mouse / resume |
| Type "showme" | open secret stats panel |

---

## Profile Data Structure

Each profile stores:

| Field | Type | Description |
|-------|------|-------------|
| id | string | unique profile ID (used to seed shop rotation and personality) |
| ownerName | string | player's name |
| hamsterName | string | hamster's name |
| hamAppearance | object | colIdx, patIdx, sizeIdx, randomized flag |
| setupChoices | object | bedding, hideout, food, water, sandbath, wheel, branch |
| setupDone | boolean | whether story + naming is complete |
| trust | number | 0–100 hidden relationship score, saved every 60s |
| moods | object | `"YYYY-M-D"` → mood ID |
| moodNotes | object | `"YYYY-M-D"` → journal text |
| careUsed | object | `"YYYY-M-D"` → array of used item IDs (includes "hold", "whistle") |
| boughtItems | array | ordered list of purchased shop item IDs |
| points | number | current point balance |
| shopState | object | `{ date, itemIds[] }` — today's 3 rotating shop picks |

---

## Room Environment

Single contained room, first-person perspective. Bounded at x: −6.6 to +6.6, z: −5.75 to +5.75.

### Permanent Features
- Hamster enclosure against the right wall — glass-fronted, wooden stand, bedding inside
- Big open windows with warm ambient light
- Soft chair and rug in the back corner
- 3 shop pedestals near the front wall (z ≈ 4.2)

### Item Locations

| Item | World Position | Notes |
|------|---------------|-------|
| Treat jar | [−3.2, 0.95, −3.4] | on a surface near cage |
| Bedding bag | [−5.6, 0.70, 2.6] | large paper bag on floor, left wall |
| Cleaning cloth | [0.6, 0.08, 0.8] | rolled cloth on floor near cage |
| Music box | [−4.2, 0.08, −1.2] | small wooden box on floor, left-center |
| Sketchbook | [−5.0, 0.05, 1.0] | flat notebook on floor, far left wall |
| Shop pedestal 1 | [−1.4, 0, 4.2] | front area |
| Shop pedestal 2 | [0, 0, 4.2] | front area, center |
| Shop pedestal 3 | [+1.4, 0, 4.2] | front area |

### Color Palette
Warm neutrals (cream, beige, soft brown) · Muted pastels (dusty pink, sage green, soft blue) · Low contrast · Soft warm sunset lighting · Slight fog at distance
