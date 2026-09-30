# Study data

These CSV files are the structured companion to the narrative [learning log](../docs/LEARNING_LOG.md) and current [study state](../docs/STUDY_STATE.md). They are designed for later summaries and charts without making each session burdensome to record.

## Files

### `study_sessions.csv`

One row per completed study session. Use `session_id` in the block file to join its work.

| Column | Meaning |
| --- | --- |
| `session_id` | Unique ID for the local date, such as `20260930-01` |
| `date` | Session date in `YYYY-MM-DD` format, using Europe/Zurich local time |
| `planned_minutes` | Planned duration, if stated at the start |
| `energy_after_1_5` | Optional self-rating: 1 = depleted, 5 = energized |
| `motivation_after_1_5` | Optional self-rating: 1 = low, 5 = high |
| `confidence_after_1_5` | Optional self-rating for the session's topic: 1 = low, 5 = high |
| `reflection` | Short user-reported reflection or tutor observation grounded in the session |
| `learning_log_ref` | Link or path to the matching narrative entry |

### `study_blocks.csv`

One row per focused activity block. Summing `minutes` gives logged time by session, topic, phase, or activity.

| Column | Meaning |
| --- | --- |
| `session_id` | ID joining to `study_sessions.csv` |
| `block_id` | Two-digit order within the session, such as `01` |
| `phase` | `phase_1` through `phase_6` |
| `activity` | `study`, `build`, `benchmark`, `review`, or `planning` |
| `topic` | Stable lowercase topic slug; see suggested vocabulary below |
| `minutes` | Actual duration for this block; blank if unknown |
| `duration_basis` | `reported_exact`, `reported_approximate`, or `not_recorded` |
| `resource` | Course, paper, documentation, or other study source, if applicable |
| `output_ref` | Repository path, commit, experiment, result, or other evidence |
| `notes` | Brief detail needed to interpret the block |

Suggested topic slugs: `ml_fundamentals`, `pytorch`, `llm_fundamentals`, `inference`, `rag`, `evaluation`, `cuda`, `triton`, `serving`, `quantization`, `career_review`, `mixed`, `unallocated`, `other`. Add a new stable slug when recurring work needs its own category.

## Recording rules

- The agent creates records when a study/build/review session ends, not when the user only asks for a recommendation.
- A user's available time at the start can populate `planned_minutes`; only the duration reported at the end counts as actual time.
- Use one block per focused topic/activity when the user provides a breakdown. If only total time is known, create one `unallocated` block instead of guessing the split.
- Use blank numeric fields for unknown values. Do not turn planned time into actual time.
- Ratings are optional and should not be requested every time. They are personal signals, not objective measures of learning.
- Keep text concise and avoid storing sensitive personal details.

## Future analysis

Once enough sessions are logged, useful views include minutes per week and phase, study versus build time, recurring topics, planned versus actual time, completed artifacts, and optional energy/motivation trends. Summaries should say how many sessions they use. Treat early patterns as provisional; do not make strong recommendations from a handful of observations.
