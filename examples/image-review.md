# Image Review Example

Input: AI-generated product photo of a person holding a futuristic smart device.

Output:

## Verdict

The image is usable as a moodboard, but not as a credible product visual. It has several visible synthetic tells.

## Visible Defects

- `Major` Right hand — the fingers appear fused near the device edge, which makes the grip look physically impossible.
- `Major` Device screen text — the tiny labels are warped and inconsistent, so the product UI reads as decorative noise.
- `Minor` Reflections — the device reflection does not match the direction of the face lighting.

## Why It Reads As AI

The image has surface polish but weak object logic. The hand, screen text, and reflections do not agree with each other.

## Fix Plan

- Crop out the hand if the product is the focus.
- Regenerate with a prompt that forbids visible microtext unless it is manually composited later.
- Retouch screen content with real UI text after generation.
