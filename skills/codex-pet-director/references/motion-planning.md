# Simple Motion Planning

Use the user's action direction and approved character reference. Read `action-guide.md` for official state names and fixed frame counts.

Write a short description or beat sheet that conveys the performance, direction and intended progression. A numbered per-frame plan is optional when it helps a difficult movement; separate key-pose generation is also optional. Do not require a full motion schema, support annotations, two endpoints, or a fixed running template for every action. Existing `motion_plan` data may be kept for compatibility, but empty fields do not prevent ordinary generation.

Let the animator choose natural intermediate poses, weight changes and timing suited to the character. Running should depict a readable alternating cycle; jumping should read as a coherent jump. Gestures, expressions and nonhuman movement need only the phases relevant to their intent. Preserve the reference character while allowing normal perspective and stylization.

Prompt with the reference, action description, angle if specified, frame count and layout. Include only a few distinctive appearance details needed to preserve identity. Keep QA instructions in `action-review.md`, not as a long negative-prompt checklist. Use one current description; resolve old conflicting beats before generation.

For a combined action, fit a readable performance into the existing state budget or explain the limitation. Do not promise unsupported runtime state chaining.

After generation, use `action-review.md` to judge actual frames and playback. A sensible alternate progression is acceptable. For a requested redo, update the affected action only and review its new result.
