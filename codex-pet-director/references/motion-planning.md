# Motion Planning Before Generation

Use this procedure for every action after character/base approval and before generating or regenerating a row. Read `action-guide.md` for fixed frame counts and `action-review.md` for review criteria. Plans guide generation; they are not evidence that generated frames passed QA.

## Build An Action Plan

Capture the desired performance, character construction, view angle, loop or one-shot behavior, and relevant contacts/support. Preserve the initial character through the approved production base and `appearance.visual_locks`; do not solve motion by redesigning anatomy. Use known user preferences without repeating the interview.

For each action record `motion_plan`:

- `intent`: concrete observable performance.
- `playback`: loop or one-shot as supported by the existing runtime.
- `constraints`: relevant canonical anatomy, proportions, material/detail locks and movement limits.
- `reference_notes`: optional motion-reference source and what it informs; reference anatomy/style must not replace the pet's design. Do not require a new reference for simple movements. For a complex unfamiliar movement, use available appropriate reference material or simplify the action rather than inventing unsupported mechanics.
- `key_poses`: numbered frame positions with pose descriptions and contact/support information.
- `frame_plan`: exactly the action's active frame count, with one description per numbered frame: pose change, participating body parts, support/contact where relevant, and arm/leg coordination where relevant.
- `qa_focus`: observable action-specific acceptance checks.

Use `beat_sheet` as the concise ordered rendering of `frame_plan`, and include the intent, keys, numbered beats, angle and relevant locks in `prompt_notes`. If structured plan and beat sheet disagree, resolve them before generation. The hatch handoff carries both; the generator must receive actual notes, not just a filename or a claim that a plan exists.

## Key Poses Then Transitions

Choose enough key poses to define the performance; do not reduce every action to two endpoints. Check key poses for reach, anatomy, balance, support/contact and clear expression before filling intermediate frames. For difficult or unapproved poses, preview representative key poses through the supported workflow when useful, and revise intent if necessary. Do not require a separate expensive image-generation round for every simple key pose.

Allocate the fixed active frame budget around meaningful phases and intended holds. Intermediate poses describe joint trajectories, weight transfer and contact changes, not a linear morph between pictures. Preserve attachments and dimensions while coordinating head, torso and limbs. Allow intentional repeated holds for still or expressive performances; do not add arbitrary movement to make every image different. For locomotion, repeated padding must not conceal missing phase coverage. Keep key and intermediate pose planning within the official format; do not introduce extra states or frames.

Examples to adapt:

- Alternating run: establish both leg-led contact/support poses and recovery phases; fill a complete cycle using the eight-frame guide in `action-review.md`, including opposing free arm swing and the loop seam.
- Full jump in the official five-frame jumping row: a compact plan can depict preparation, push-off/lift, airborne pose, landing, and settling. This is an example, not mandatory uniform timing. Check that the chosen range and playback make the compact sequence readable; do not force this if the approved jumping performance is a small reaction or a non-legged gesture.
- Four-frame greeting: raise/prepare, greeting gesture, continuation/hold, release or return appropriate to actual playback. Adapt to existing rounded appendages, wings, head or body without inventing hands.
- Blink/idle: anchor open/closed/reopened expression and breathing/hold as applicable. Maintain facial identity; do not force contact/support fields where irrelevant.
- Prop or headwear interaction: preparation, coordinated approach, contact, optional hold, release and recovery distributed within the state's existing budget. Move the body naturally instead of elongating an appendage.

## Compound Motions

For a user-requested combination such as run then jump, clarify the intended official slot or runtime sequence only if not inferable. Existing directional running and jumping states are separate; do not promise automatic state chaining or custom triggers that the runtime does not support. A combined performance inside one approved row must fit that row's fixed budget and preserve the slot's intent. Plan entry, change of support/propulsion, landing/recovery and exit as one coherent sequence. Do not simply concatenate two independently aligned loops. If the sequence cannot read within the available frames, propose a simpler version or supported separate actions and explain the limitation.

## Generate And Compare

Pass canonical reference, locks and the complete numbered plan to hatch-pet's supported row workflow. Do not build an alternative image/morph pipeline. After generation, inspect all actual lossless frames and temporal playback using `action-review.md`. Compare observed poses to intended phases; accept an alternate valid pose progression if it satisfies intent and constraints, not merely exact wording. Record concrete failures and affected frame numbers. Structural script success or a plausible plan alone never establishes motion correctness.

For each redo update only the affected plan/notes, invalidate that artifact's QA and acceptance, preserve accepted versions and unaffected rows, then re-generate and re-review. Aggregate observed defects before one targeted correction. If it still fails, show evidence and next options instead of unlimited automatic retries. Distinguish blocking defects (identity/anatomy/proportion drift, incoherent motion/contact, severe blur) from optional acting preferences; subjective preferences alone should not repeatedly fail technical QA.
