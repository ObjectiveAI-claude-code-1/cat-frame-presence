# cat-frame-presence

A scalar function that measures how commandingly a cat occupies the frame of a photograph.

## Overview

Not every photo of a cat is a photo *of* a cat. Sometimes the cat is a speck on a hillside. Sometimes it's a sliver at the edge of a room. Sometimes a tight crop captures fur and whiskers but loses the animal entirely. `cat-frame-presence` quantifies the difference — it asks whether the cat commands its frame, and answers with a single number between 0 and 1.

A score near **1** means the cat is unmistakably the subject: large, fully visible, and authoritatively placed within the image. A score near **0** means the cat is incidental: small, distant, fragmented by cropping, or lost in a composition that wasn't arranged around it.

## Input

The function accepts a single required field:

| Field | Type | Required | Description |
|-------|------|----------|-------------|
| `image` | image | Yes | A photograph or image containing a cat. |

The image may come from any source — a professional portrait, a casual phone snapshot, a surveillance still, a frame extracted from video, or a cropped region of a larger scene. The function does not evaluate aesthetic merit, image quality, or the beauty of the cat itself. It concerns itself solely with the spatial and compositional relationship between the cat and the rectangular boundaries of the image.

## Output

A scalar value in the range **[0, 1]**, representing the degree to which the cat commands its frame.

| Score Range | Interpretation |
|-------------|---------------|
| **0.8 – 1.0** | The cat dominates the frame — large, whole, and deliberately placed. The image feels built around the cat. |
| **0.6 – 0.8** | The cat has strong presence — it fills a generous portion of the frame and reads as a complete, well-situated subject. |
| **0.4 – 0.6** | Moderate presence — the cat is visible and recognizable but may be somewhat small, partially cropped, or not ideally composed. |
| **0.2 – 0.4** | Weak presence — the cat is small, noticeably cropped, or awkwardly placed. It does not command the viewer's attention. |
| **0.0 – 0.2** | Minimal presence — the cat is tiny, severely fragmented, or lost in the composition. The frame was not made for this cat. |

## What It Evaluates

The final score is a weighted blend of three distinct evaluations, each capturing a different dimension of what it means for a cat to be present in its frame.

### 1. Proportional Scale

How much of the total image area the cat physically occupies. This is the foundational measurement — the ratio of the cat's visible extent to the available frame space. A cat that fills a generous share of the image is inherently more present than one that appears small or distant. Without sufficient scale, no amount of compositional care can make a cat feel commanding.

- **Scores high** when the cat is large and takes up a substantial portion of the frame.
- **Scores low** when the cat is tiny, far away, or occupies only a sliver of the image.

### 2. Completeness of Form

Whether the cat's body reads as whole and uninterrupted within the image boundaries, or whether the frame has cropped or severed the subject. A cat shown from head to tail — or naturally curled so that its full form is implied — is complete. A cat whose head is cut off, whose body is sliced by the frame edge, or that is reduced to a disembodied fragment is incomplete.

The key distinction is between the frame *containing* the cat and the frame *interrupting* the cat. A cat with paws tucked beneath its body is complete; a cat whose torso is arbitrarily severed at the image border is not. This quality ensures the function does not confuse proximity with presence.

- **Scores high** when the cat appears entirely and comfortably captured within the frame.
- **Scores low** when cropping makes the subject feel truncated, severed, or fragmentary.

### 3. Visual Authority

Whether the cat feels deliberately and comfortably situated in the composition — as though the image was arranged around the cat — or whether its position feels incidental, cramped, or accidental. A cat with balanced space around it, occupying the frame with a sense of intentional staging, commands authority. A cat shoved into a corner, pressed against an edge, or caught at an undermining angle lacks authority regardless of size or completeness.

This is the quality that separates a portrait from a snapshot. It captures whether the cat's placement within the rectangle feels purposeful.

- **Scores high** when the cat's placement feels deliberate and the composition serves the subject.
- **Scores low** when the framing feels haphazard or the cat appears subordinate to the space around it.

## Use Cases

- **Photo curation and filtering**: Automatically select images where the cat reads clearly as the subject — ideal for profile pictures, thumbnails, and feature images that must work at any display size.
- **Automated photography**: Help camera systems or burst-mode selectors decide whether a captured frame is worth keeping, or whether to wait for the subject to fill the frame more completely.
- **Ranking and sorting**: Score and rank cat photographs for social media feeds, stock photography libraries, or content recommendation systems where strong subject presence drives engagement.
- **Quality gating**: Set minimum presence thresholds to reject images where the cat is too small, too cropped, or too poorly composed to serve as a primary subject image.