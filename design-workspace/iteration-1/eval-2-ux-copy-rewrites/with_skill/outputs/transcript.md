# Execution Transcript — eval-2-ux-copy-rewrites (with_skill)

## Task

Rewrite two login form error messages and suggest a submit button label.

## Skill Loaded

`/Users/exodes/Projects/skills-workspace/design/SKILL.md`

## Execution Steps

### 1. Load SKILL.md

Read `/Users/exodes/Projects/skills-workspace/design/SKILL.md`.

Routing table identified: prompt asks to "write copy / error messages / CTA" → load `references/ux-copy.md`.

### 2. Load Reference File

Read `/Users/exodes/Projects/skills-workspace/design/references/ux-copy.md`.

Key principles applied:

- Error message pattern: **What happened + Why + How to fix**
- Voice/tone: **Empathetic and helpful** for errors; **specific and action-oriented** for CTAs
- CTA pattern: start with a verb, be specific, match the outcome to the label

### 3. Analyze Input Copy

| Original                    | Problem                                                                        |
| --------------------------- | ------------------------------------------------------------------------------ |
| `'Error occurred.'`         | Vague — no field named, no cause, no fix; sounds like a system fault           |
| `'Invalid input detected.'` | Robotic — no field named, no format guidance, passive/machine-language framing |
| Submit button: unspecified  | Needs a verb label matching the action                                         |

### 4. Apply Copy Framework

**Wrong credentials error:**

- What happened: credentials didn't match
- Why: email or password incorrect (deliberately ambiguous for security)
- How to fix: check and try again
- Result: "Incorrect email or password. Please check and try again."

**Invalid email format:**

- What happened: email field lacks `@`
- Why: format doesn't match expected pattern
- How to fix: enter a valid email — show example
- Result: "Please enter a valid email address (e.g. name@example.com)."

**Submit button:**

- Action: authenticate / log in
- Convention: "Log in" is the standard; "Submit" is a non-action form artifact
- Result: "Log in"

### 5. Generate Output

Followed the output template from `ux-copy.md`:

- Recommended copy (primary picks)
- Alternatives table (3 options per element with tone + use case)
- Rationale (why each rewrite works)
- Localization notes

### 6. Save Output

Written to: `with_skill/outputs/response.md`

## Skill Reference Files Used

- `design/SKILL.md` — routing
- `design/references/ux-copy.md` — principles, patterns, output template
