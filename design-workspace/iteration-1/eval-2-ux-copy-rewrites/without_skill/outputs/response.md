# UX Copy Rewrites — Response (No Skill / Baseline)

## Prompt

Our login form has these two error messages and I'm not sure they're good. First one: 'Error occurred.' — shown when the email/password combo is wrong. Second one: 'Invalid input detected.' — shown when the email field has no @ sign. Can you rewrite these and also suggest what the submit button should say?

---

## Response

Here are improved versions of both error messages and a button label suggestion:

---

### Error 1: Wrong email/password combination

**Current:** `Error occurred.`

**Suggested:** `Incorrect email or password. Please try again.`

- Tells the user exactly what went wrong
- Avoids vague language ("error occurred" could mean anything)
- Avoids confirming which field is wrong (security best practice — don't tell attackers whether the email exists)

---

### Error 2: Invalid email format (missing @)

**Current:** `Invalid input detected.`

**Suggested:** `Please enter a valid email address (e.g. name@example.com).`

- Explains what's wrong in plain language
- Gives a concrete example so users know the expected format
- Removes jargon ("detected" sounds automated and cold)

---

### Submit button label

Options ranked by preference:

1. `Sign In` — clearest, most conventional for login flows
2. `Log In` — also common, slightly more informal
3. `Continue` — works if login is a step in a larger flow
4. Avoid: `Submit` — generic, doesn't tell the user what action they're taking

**Recommendation:** Use `Sign In` unless your product uses "Log In" consistently elsewhere — pick one and stick to it.
