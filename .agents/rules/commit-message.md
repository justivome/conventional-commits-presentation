---
trigger: always_on
---

Your task is to help the user to generate a commit message and commit the changes using git.

## Guidelines

- DO NOT add any ads such as "Generated with [Claude Code](https://claude.ai/code)"

- Only generate the message for staged files/changes

- **NEVER STAGE FILES** - The user must stage files manually. The assistant is strictly prohibited from staging any files, even if they appear related to the current task.

- **NEVER commit `.windsurf/COMMIT_MSG`** - this is a temporary file and must remain local only

- Follow the rules below for the commit message.

## Format

```none
#<ticket-number> - <type>:<space><message title>



<bullet points summarizing what was updated>

```

## Example Titles

```none
#CALI-3250 - feat(auth): add JWT login flow

#CALI-1234- fix(ui): handle null pointer in sidebar

#CALI-5678 - refactor(api): split user controller logic

#CALI-9999 - docs(readme): add usage section
```

## Example with Title and Body

```none
#CALI-3250 - feat(auth): add JWT login flow

- Implemented JWT token validation logic
- Added documentation for the validation component
```

## Rules

- Always start with ticket number: `#<ticket-number>`
- If no ticket number provided, use current branch name (e.g., CALI-3250 -> #CALI-3250)
- title is lowercase, no period at the end.
- Title should be a clear summary, max 50 characters.
- Use the body (optional) to explain _why_, not just _what_.
- Bullet points should be concise and high-level.

Avoid

- Vague titles like: "update", "fix stuff"

- Overly long or unfocused titles

- Excessive detail in bullet points

## Allowed Types

| Type     | Description                           |
| -------- | ------------------------------------- |
| feat     | New feature                           |
| fix      | Bug fix                               |
| chore    | Maintenance (e.g., tooling, deps)     |
| docs     | Documentation changes                 |
| refactor | Code restructure (no behavior change) |
| test     | Adding or refactoring tests           |
| style    | Code formatting (no logic change)     |
| perf     | Performance improvements              |
 