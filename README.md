# Mano-Action: Self-Reinforcement for GUI Grounding

GUI grounding maps natural-language instructions to precise UI actions and coordinates. We introduce a bidirectional, cycle-consistent self-reinforcement approach that boosts robustness to varied phrasing and improves localization accuracy—without extra manual labels.

## Core Idea
Learn both directions to form a round trip:
- Text → Click: predict the target element and its coordinates.
- Click → Text: describe the element at the given coordinates.
If the round trip stays consistent (text → click → text or click → text → click), the model is rewarded. This encourages diverse, accurate descriptions and sharper localization.

## Training Overview
- SFT warm-up: bidirectional supervision so the model can both localize and describe.
- RL self-reinforcement: generate multiple descriptions per target, re-localize, and optimize with dual rewards:
  - Localization reward: does the predicted click hit the correct element?
  - Semantic reward: do the generated descriptions faithfully match the element?

## Benefits
- More robust to wording changes and paraphrases.
- Better exploration before RL, leading to stronger refinement.
- Parameter-efficient improvements in click precision.

## Results
State-of-the-art among comparable-size models on four GUI grounding benchmarks, validating the effectiveness of the bidirectional, cycle-consistent paradigm.
