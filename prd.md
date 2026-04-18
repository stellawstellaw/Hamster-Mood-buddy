Product Requirement Document:

I want a 3d game based on three.js

My game will be about hamsters

Game Name: Fluffy Little Hamster

Style:
🎨 GAME AESTHETICS + UI STYLE BRIEF
🌼 Overall Emotional Tone

This game should feel:

soft
safe
quiet
cozy
emotionally gentle

The player should feel like:
“I can exist here without pressure.”

Avoid anything that feels:

loud
overly game-like
stressful
cluttered
overly bright or saturated
🏡 Environment Style (3D World)
Small, cozy room (intimate scale, not large spaces)
Warm lighting (soft yellows, sunset tones, gentle shadows)
Slightly stylized, not hyper-realistic
Soft edges, rounded shapes where possible
Lived-in feeling (blankets, desk items, subtle clutter)
Color Palette:
Warm neutrals (cream, beige, soft brown)
Muted pastels (dusty pink, sage green, soft blue)
Low contrast, nothing harsh
🐹 Hamster Visual Style
Slightly stylized and soft (not realistic fur simulation)
Round shapes, small proportions
Smooth/simple animations with gentle motion
Movement should feel light and natural, not snappy
💬 UI DESIGN PRINCIPLES
Core rule:

UI should feel like it “belongs” in the world, not like a game overlay.

✨ UI Style
Minimal and uncluttered
Rounded corners
Soft drop shadows or blur backgrounds
Semi-transparent panels (like frosted glass)
Gentle fade-in / fade-out animations
🎨 UI Colors
Match environment palette
Avoid pure white or pure black
Use soft off-white and warm gray instead
Accent colors should be muted pastel tones
🔤 Typography
Simple, clean sans-serif font
Slightly rounded feel if possible
Medium weight (not too thin, not bold-heavy)
Plenty of spacing between lines

Tone should feel:

calm
quiet
not “app-like” or corporate

🌼 1. High Concept

A first-person 3D life simulation where the player shares a small space with a hamster companion. The player performs a daily emotional check-in (“talking to the hamster”) and builds a relationship over time through consistent interaction.

The hamster responds through behavior only, and gradually adapts as it learns whether the player is safe, present, and consistent.

🎯 2. Core Design Principles
No punishment systems
No failure states
No forced interaction
No streak pressure
No direct emotional labeling of the player

The experience is driven by:

daily mood input
behavioral AI response
hidden trust progression
👤 3. Player Perspective
First-person only
Player exists inside a single room environment
Interaction is through movement and simple interaction prompts
🏡 4. Core Environment

Single contained space:

one main room
hamster area/enclosure zone by wall
interactable objects for basic care actions
Big, open windows that let in light
soft, realistic lighting, not overdoing it
a soft chair and rug in the back
No open-world or multi-area structure required for MVP.

🐹 5. Hamster System (CORE ENTITY)

The hamster is a simulated agent driven by weighted behavioral AI, not scripted states.

🧠 Internal Variables (Hidden)
Trust (0–100)
Energy (0–100)
Curiosity (0–100)
Stress (0–100)
🧠 Behavior Model

The hamster does NOT use fixed state → action mappings.

Instead it uses a desire-based system:

Possible behaviors:
explore room
touch and rub cage glass
approach player
stay near player
hide in safe zone
idle/rest
interact with objects
burrow

Each behavior is scored dynamically:

score = baseWeight + trustModifier + moodBias + randomness + memoryBias

The hamster selects behaviors using weighted probability or highest scoring option.

🎲 Required AI Rules
Must include randomness in decision making
Must avoid repeating the same location consecutively
Must use random navigable points within bounds (not fixed positions)
Must include pauses and hesitation behavior
Must simulate micro-movement variation
Must include memory of previously visited zones
💬 6. DAILY MOOD SYSTEM (“TALKING TO HAMSTER”)
Core Loop Feature:

Once per in-game day, the player inputs a mood representing how they feel and can write about why which is "talking" to the hamster, and the hamster will listen to the player with a cute animation and gain a few trust points depending on how much they talk.

Input:
Single mood selection (required)
Mood set (initial MVP):
Calm
Happy
Tired
Anxious
Overwhelmed
Neutral
Nervous
Excited
Sad

Optional extension:

short text input (not required for MVP)
System Function:

Mood does NOT directly control behavior.

Instead it:

modifies behavior weights for that day
slightly influences hamster proximity tendencies
affects trust growth rate subtly
🐹 7. HAMSTER RESPONSE SYSTEM

The hamster reacts to player mood through:

movement patterns
proximity to player
exploration tendency
resting frequency
interaction initiation
Key Rule:

No dialogue or explicit feedback about player emotions.

All response is indirect and behavioral.

💛 8. TRUST SYSTEM (HIDDEN PROGRESSION)

Trust is a hidden relationship variable that evolves over time.

Trust increases through:
consistent daily check-ins
calm, non-aggressive interaction patterns
time spent in shared space
repeated safe interactions
Trust stages:
Stage 1 — Unfamiliar
cautious movement
avoids close proximity
high alert idle behavior
Stage 2 — Curious
begins observing player more often
occasional approach behavior
reduced avoidance
Stage 3 — Comfortable
shares space more consistently
approaches player voluntarily
reduced hesitation in movement
Stage 4 — Trusting Companion
frequent proximity to player
stable calm behavior
occasional following behavior
Important:

Trust is NOT shown directly to the player.

📊 9. MOOD HISTORY SYSTEM
Feature:

Stores all past daily mood entries.

Data stored per entry:
date
selected mood
hamster behavioral state snapshot (optional)
trust level snapshot (internal only)
Access:

Player can view past entries in a historical format, colour coded and also showing what they wrote.

Rules:
no judgment indicators
no ranking or scoring
no “good/bad” classification
🔁 10. CORE GAME LOOP
Enter environment (first-person)
Observe hamster current behavior
Perform daily mood input (“talking”)
System updates behavioral weights
Hamster responds dynamically
Optional interaction actions
Save mood + update history + adjust trust
End session / return later
🎬 11. GAME START FLOW
First-person spawn in room
Hamster already present in environment
Player gains movement control immediately
Hamster performs initial idle behavior
Player approaches interaction zone
Mood input system becomes available
First mood is recorded
Behavioral response system activates
🔍 12. Personality & Preference Discovery System

The hamster has hidden personality traits and preferences that are not shown directly to the player.

Hidden Personality Traits:
Shy ↔ Bold
Curious ↔ Cautious
Social ↔ Independent
Playful ↔ Calm
Sensitive ↔ Stable

These exist as continuous values (0–100 sliders), not fixed labels.

Hidden Preferences:
favorite foods / treats
preferred bedding types
preferred activity levels
safe / comfort zones in the room
interaction tolerance (how often it likes attention)
How the player discovers them:

The player learns through repeated observation of:

movement patterns
reactions to mood inputs
responses to care actions
proximity behavior changes over time
repeated environmental preferences (where it rests, returns, avoids)
Core rule:

Nothing is explicitly revealed to the player.
All understanding is inferred gradually.

Emotional purpose:

The system creates the feeling of:

“I slowly understand this little creature without being told.”

🧸 13. Care & Bonding System

The player can perform optional care actions to build a bond with the hamster over time.

Care is not required for progression and does not create punishment loops.

Care Actions:
feeding treats
changing bedding
gentle holding / interaction
cleaning hamster environment
System behavior:

Care actions:

slightly increase trust
influence comfort behavior
affect long-term preference learning
adjust hamster proximity behavior indirectly
Core rule:

Care is optional and non-pressuring.
Missing care does NOT cause negative states.

Emotional purpose:

The system creates the feeling:

“small things I do gently matter over time.”

🧱 14. DEVELOPMENT STAGES (CLAUDE-READY BREAKDOWN)
🥇 STAGE 1 — First-Person Base System
Tasks:
Implement first-person movement controller
Add camera system
Build basic room layout
Add collision and navigation boundaries
Output:

Player can freely move in environment.

🥈 STAGE 2 — Hamster Entity + Movement
Tasks:
Add hamster model
Implement idle animation system
Implement basic movement system using navmesh
Add random wandering behavior
Output:

Hamster exists and moves autonomously.

🥉 STAGE 3 — Behavior AI System (CORE)
Tasks:
Implement weighted behavior system
Define behavior list (explore, idle, approach, hide, interact)
Add scoring system:
base weight
trust modifier
mood modifier
randomness
Implement decision loop
Output:

Hamster behavior is dynamic and non-scripted.

🏅 STAGE 4 — Daily Mood Input System
Tasks:
Create daily input trigger system
Implement mood selection interface logic
Save selected mood per in-game day
Link mood input to AI modifiers
Output:

Player can “talk” to hamster once per day.

📊 STAGE 5 — Mood History System
Tasks:
Save daily mood entries
Store mood + date + metadata
Implement retrieval system for past entries
Display historical data in sequence
Output:

Player can review emotional history.

🧠 STAGE 6 — Trust System
Tasks:
Implement hidden trust variable
Define trust gain rules
Connect trust to AI behavior weights
Add trust-based behavioral stages
Output:
Hamster relationship evolves over time.

🧸 STAGE 7 — CARE & BONDING SYSTEM
Implement care interactions: feeding, bedding changes, holding, cleaning
Track care history (type, frequency, timing)
Connect care actions to trust growth (soft influence, not primary driver)
Integrate care history into AI behavior weighting (comfort, proximity, exploration bias)
Add limits/soft caps to prevent farming or spam interactions from boosting trust too fast
Ensure hamster reacts behaviorally (not verbally) to care actions


🔍 STAGE 8 — PERSONALITY & PREFERENCE DISCOVERY SYSTEM
Implement hidden hamster personality variables (continuous sliders, not labels)
Implement hidden preference variables (food, bedding, interaction style, comfort zones)
Ensure personality affects AI behavior weights (exploration, shyness, social behavior, etc.)
Track repeated player interaction patterns and hamster responses over time
Allow personality and preferences to be inferred only through behavior (no UI reveal)
Add gradual behavior consistency so traits become clearer over time but never explicitly shown
Ensure system creates emergent “learning the hamster” behavior loop

⚙️ STAGE 9 — AI POLISH LAYER
Tasks:
Add movement randomness tuning
Add hesitation / pause system
Add zone memory system
Prevent repetitive movement loops
Output:

Hamster feels less robotic and more organic.

🚀 16. MVP DEFINITION (MINIMUM SHIPPABLE GAME)

Game is considered complete when:

First-person movement works
Hamster exists with autonomous AI behavior
Daily mood input system works
Mood affects hamster behavior
Trust system changes behavior over time
Mood history is saved and viewable
🧠 FINAL SUMMARY

This game is a first-person emotional life simulation where a hamster companion responds to daily mood input through a weighted behavioral AI system. The relationship evolves through hidden trust mechanics and long-term interaction patterns rather than explicit goals or failure states.

