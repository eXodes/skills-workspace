## UX Copy: Login Form — Error Messages & Submit Button

### Recommended Copy

**Wrong email/password error**: "Incorrect email or password. Please check and try again."

**Invalid email format error**: "Please enter a valid email address (e.g. name@example.com)."

**Submit button**: "Log in"

---

### Alternatives

| Option | Copy                                                                             | Tone            | Best For                                                       |
| ------ | -------------------------------------------------------------------------------- | --------------- | -------------------------------------------------------------- |
| A      | "Incorrect email or password. Please check and try again."                       | Neutral, direct | Most login forms; balances clarity with brevity                |
| B      | "We didn't recognize that email or password. Try again, or reset your password." | Warmer, helpful | Apps with a friendly/consumer tone; surfaces the recovery path |
| C      | "Email or password doesn't match our records."                                   | Formal          | Enterprise/B2B products with a more formal voice               |

| Option | Copy                                                                    | Tone           | Best For                                      |
| ------ | ----------------------------------------------------------------------- | -------------- | --------------------------------------------- |
| A      | "Please enter a valid email address (e.g. name@example.com)."           | Instructional  | Clear format guidance with a concrete example |
| B      | "That doesn't look like an email address — make sure it includes an @." | Conversational | Consumer apps with a warmer voice             |
| C      | "Enter a valid email address."                                          | Terse          | Space-constrained inline validation labels    |

| Option | Copy       | Tone              | Best For                                      |
| ------ | ---------- | ----------------- | --------------------------------------------- |
| A      | "Log in"   | Standard, neutral | Most products — matches expected convention   |
| B      | "Sign in"  | Slightly warmer   | Consumer apps; "sign in" feels less technical |
| C      | "Continue" | Progressive       | Multi-step flows where login is one step      |

---

### Rationale

**'Error occurred.' → 'Incorrect email or password. Please check and try again.'**

The original is a dead end — it tells the user something went wrong but not what or how to fix it. The rewrite names the specific inputs that failed (email or password), removes any implication of a system fault (it's not an "error," the credentials just didn't match), and closes with a concrete action. Security note: deliberately saying "email or password" rather than singling out one avoids confirming whether an account exists for a given email address — a minor but meaningful security practice for login forms.

**'Invalid input detected.' → 'Please enter a valid email address (e.g. name@example.com).'**

"Invalid input detected" reads like a system log, not a message to a human. It names neither the field nor the problem, so users have to guess what to fix. The rewrite identifies the exact field (email), explains the required format by example, and removes the passive/robotic framing. The example `name@example.com` is especially useful for users unfamiliar with email address format conventions.

**Submit button: 'Log in'**

Generic labels like "Submit" or "Go" tell the user nothing about what happens next. "Log in" names the action precisely, matches what users expect from login forms across the web, and is more scannable than the two-word alternative "Sign in" (though either works). Avoid "Submit" — it's a form artifact, not a user action.

---

### Localization Notes

- "Log in" vs "Sign in": these are effectively interchangeable in English but pick one and use it consistently across the product (button, nav links, email subject lines, etc.)
- The email example `name@example.com` uses `example.com`, an IANA-reserved domain — safe to use in documentation and UI; avoid real domains
- Character expansion for Romance languages (French, Spanish, Italian) is typically 20–30% — inline validation messages should have layout room to grow
- "Incorrect email or password" translates well across major languages; avoid idioms or contractions that may not carry over
- Error messages using "we" (e.g. Option B: "We didn't recognize…") require extra care in localization — some markets find the first-person brand voice unusual or overly casual
