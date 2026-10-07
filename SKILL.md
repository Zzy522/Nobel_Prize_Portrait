---
name: nobel-prize-portrait
description: Generate an artistic Nobel Prize announcement portrait from an uploaded person photo, using expressive black ink, sparse ochre-gold accents, warm ivory paper, and an editorial hand-drawn aesthetic. Use when a user asks to turn a person image into a Nobel Prize portrait, laureate-style illustration, academic award artwork, or a similar artistic ink-and-gold portrait; support loose identity interpretation, adjusted hairstyle, subtle smiling or humorous expressions, and optional style-reference images.
---

# Nobel Prize Portrait

Turn a supplied person image into a single, polished Nobel Prize announcement style portrait. Use the built-in `image_gen` tool for the actual generation or edit; do not use a CLI fallback unless the user explicitly requests it.

## Workflow

1. **Identify the inputs.** Treat the person's photo as the subject/identity reference. If the user supplies one or more example artworks, treat them as style references. If an edit source is explicitly specified, use that exact source and do not substitute another conversation image.
2. **Inspect local images first.** Use `view_image` on every local input before editing. If every required image has a local path, pass them through `referenced_image_paths`; otherwise use the smallest `num_last_images_to_include` value that includes all required conversation images.
3. **Choose identity fidelity.** Default to moderate fidelity: preserve the broad age, gender presentation, recognizable face cues and overall pose, while allowing artistic changes to face proportions, hairstyle and clothing details. If the user says “保留本人特征” or asks for a realistic portrait, increase fidelity. If the user asks for an artistic or laureate-like image, permit visible reinterpretation.
4. **Generate one portrait.** Unless the user requests a group, create one centered head-and-shoulders portrait in a vertical 4:5 composition with clean margins. Keep the artwork free of text, logos, medals, names and watermarks.
5. **Inspect and refine once if needed.** Check that the output reads as a hand-drawn Nobel announcement illustration rather than a photo filter. If it is too photorealistic, too densely shaded, or too literal, run one targeted edit emphasizing sparse linework, paper-white areas and graphic gold shapes.
6. **Return the generated image inline.** Briefly state what was changed. Do not burden the user with the internal prompt or file path unless they request it.

## Core visual direction

Use the supplied artwork references as visual guidance without copying their text, exact people, logos or layout:

- warm ivory, lightly textured paper
- confident black ink contours with varied stroke weight
- selective matte ochre-gold shadow shapes around the temples, brows, nose, cheek edges, ears and under the chin
- large unpainted paper-white areas on the forehead, cheeks, shirt and jacket
- expressive but economical facial marks; mild asymmetry is welcome
- rhythmic, separated hair strokes with visible white gaps; adjust the hairstyle artistically when requested
- simple outlined collar, jacket and tie; avoid a fully black, heavily shaded suit
- restrained academic dignity with a little personality

Avoid photorealistic skin rendering, glossy digital painting, gradients, dense all-over crosshatching, metallic gold, anime styling, broad caricature, extra people, text, award emblems, medals, signatures and watermarks.

## Expression and personality controls

When the user asks for a smile or a humorous tone, use a small closed-mouth smile, gently raised mouth corners, warm eyes and a quietly amused expression. Keep it suitable for an official portrait: avoid a broad grin, visible teeth emphasis, winking, meme-like exaggeration or slapstick features.

When the user asks for stronger artistic expression, loosen identity preservation, simplify facial planes, allow a slightly elongated or sculptural face, exaggerate the hair silhouette modestly and use confident irregular ink contours. Do not turn the person into an unrelated character.

## Prompt template

Shape the image-generation prompt around these requirements:

```text
Create one artistic Nobel Prize announcement portrait from the supplied person image.
Use the person photo as the subject reference and any additional artwork as style reference.
Preserve [moderate / high / loose] identity fidelity according to the user request.
Render a centered head-and-shoulders portrait on warm ivory paper in expressive black ink
with sparse ochre-gold watercolor shapes, large paper-white areas, lively hand-drawn contours,
and a refined editorial academic mood. Artistically adjust the hairstyle if requested.
For a smile request, use a subtle closed-mouth smile and quietly amused eyes while keeping
the expression dignified. Use a vertical 4:5 composition with clean margins.
Exclude all text, names, logos, medals, emblems, signatures, watermarks, extra people,
photorealism, glossy gradients and dense crosshatching.
```

## Failure handling

- If the image cannot be read, ask the user to re-upload it rather than inventing the person's appearance.
- If several people appear and the primary subject is unclear, ask which person to use before generating.
- If the style reference contains lettering or recognizable award branding, reproduce only the visual language and omit the lettering and branding from the output.
- If the user asks for a different mood, change expression, line energy and palette while retaining the core Nobel editorial illustration structure unless they explicitly ask to replace it.
