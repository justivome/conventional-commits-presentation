---
description: Commit staged git changes
---

# Commit Workflow

This workflow helps you commit staged changes using the standardized commit message format.

## Steps

1. **Verify files are staged**
   - User must stage files manually before running this workflow
   - Only staged changes will be committed
   - **ASSISTANT MUST NEVER STAGE FILES** - this is strictly prohibited

2. **Get staged changes and analyze**
   - Use the git MCP tool to get the current staged diff
   - Analyze the changes to generate an appropriate commit message

3. **Generate commit message**
   - Get ticket number from branch name if not provided
   - Use the @commit-message rule to create a properly formatted commit message
   - Follow the format: `#<ticket-number> - <type>(<scope>): <message title>`
   - Add optional bullet points explaining what was changed

4. **Show commit message for review**
   - Display the proposed commit message in the chat inside markdown code block that I can copy
   - Ask: "Reply with 'proceed', 'commit', or 'go' to commit, or provide modifications"
   - User can request modifications including removing the body (title-only commits)
   - **STOP and wait for user response**
   - **Do NOT create any files or commit yet**

5. **Commit after user approval**
   - If user says "proceed", "commit", "go", similar, or pastes exact commit message:
     - **Immediately** run the commit using the git MCP tool with the message from step 3
     - **Do NOT ask for additional confirmation**
   - If user requests modifications:
     - Apply the requested changes to the commit message
     - Show the updated message and wait for confirmation again
     - Once approved, commit with the modified message

6. **Output Message**
   - After committing, return EXACTLY this markdown (copy the structure exactly):
   - **Successful Format** (if commit succeeds):

   ````md
   ## ✅ Committed successfully

   - Branch: `<branch-name>`
   - Hash: `<commit-hash>`
   - Files changed: **<n>** | Insertions: **<+n>** | Deletions: **<-n>**

   * **Error Format** (if commit fails):

   ```md
   ## ❌ Commit failed

   - Branch: `<branch-name>`
   - Error: `<error-message>`
   ```
   ````

## Commit Message Format

```none
#<ticket-number> - <type>(<scope>): <message title>

- Brief summary of changes (optional)
- Another key change if needed (optional)
```

## Common Types

- `feat`: New feature
- `fix`: Bug fix
- `refactor`: Code restructure
- `docs`: Documentation changes
- `test`: Test additions/changes
- `chore`: Maintenance tasks
- `style`: Code formatting
- `perf`: Performance improvements

## Important Notes

- Always start with ticket number: `#<ticket-number>`
- If no ticket number provided, use current branch name (e.g., CALI-3250 -> #CALI-3250)
- **User must stage files manually** - assistant will NOT stage files automatically
- **ASSISTANT IS STRICTLY PROHIBITED FROM STAGING FILES** - even if files appear related
- **Exception:** The `/patch` workflow is the only approved bypass — the assistant MAY stage ONLY `package.json` exclusively within that workflow
- Only commits **staged** changes
- Title must be lowercase, max 50 characters, no period
- Bullet points should be concise and high-level
- Focus on what changed, not why (save that for PR descriptions)
- Commit message is shown in chat for review - no file approval needed

## Example

```none
#CALI-3250 - feat(auth): add JWT login flow

- Implemented JWT token validation logic
- Added login form component
- Updated auth service methods
```
 