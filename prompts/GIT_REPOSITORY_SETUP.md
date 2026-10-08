# GIT REPOSITORY SETUP - PLANNER INSTRUCTIONS

## Objective

Prepare the existing local Playwright project for the public GitHub repository:

https://github.com/sai-18QA/salesforce-hybrid-automation-framework.git

The objective of this phase is ONLY to safely prepare, commit, and push the existing project from the local repository to the GitHub remote repository.

Do NOT start Salesforce framework implementation during this phase.

---

## 1. Inspect the Current Git Repository

First inspect the current project and determine:

- Whether Git has been initialized
- Current Git branch
- Current Git status
- Configured Git remote
- Tracked files
- Modified files
- Staged files
- Untracked files

Do not make assumptions about the current Git state.

---

## 2. Identify All Untracked Files

Review every untracked file in the project.

Categorize each file as:

### A. Safe to commit

Files required for the Playwright project and framework.

Examples:

- package.json
- package-lock.json
- playwright.config.ts
- tsconfig.json
- tests
- .gitignore
- .env.example
- prompts
- .vscode configuration that does not contain secrets

### B. Must NOT be committed

Examples:

- .env
- node_modules/
- auth/
- storage state files
- test-results/
- playwright-report/
- credentials
- passwords
- API keys
- access tokens
- client secrets
- database credentials
- temporary/generated files

### C. Requires human approval

Any unexpected file whose purpose or contents cannot be confidently determined.

If a potentially sensitive file is found, STOP before staging it and ask for human approval.

---

## 3. Review .gitignore

Verify that the project has an appropriate .gitignore.

At minimum, ensure these are ignored:

.env
auth/
node_modules/
playwright-report/
test-results/

Also ensure that authentication/session files and other sensitive files cannot accidentally be committed.

Do not remove existing valid .gitignore entries.

---

## 4. Protect Environment Variables

Check whether .env exists.

If .env exists:

- Confirm it is ignored by Git.
- Do NOT display its contents.
- Do NOT expose passwords or secrets.
- Do NOT stage it.
- Do NOT commit it.

The real .env file must remain local.

---

## 5. Create .env.example if Required

Check whether .env.example exists.

If it does not exist, create it with placeholders only:

SF_BASE_URL=
SF_USERNAME=
SF_PASSWORD=

Do NOT put real Salesforce credentials into .env.example.

---

## 6. Review the Staging Set

Before committing, review exactly which files will be committed.

Do NOT blindly execute:

git add .

without first understanding the untracked files.

The staging area must NOT contain:

- .env
- passwords
- access tokens
- API keys
- database credentials
- storage state
- authentication files
- node_modules
- test-results
- playwright-report

---

## 7. Stage the Safe Files

Stage only the files that are safe and required for the project.

Then verify:

git status

Confirm that sensitive files are not staged.

---

## 8. Create the Initial Commit

Create the initial commit using:

git commit -m "Initial Playwright framework setup"

---

## 9. Configure the Main Branch

Ensure the local branch is named:

main

If required, use:

git branch -M main

---

## 10. Configure the GitHub Remote

The required remote repository is:

https://github.com/sai-18QA/salesforce-hybrid-automation-framework.git

Verify the remote using:

git remote -v

If the correct remote is not configured, configure it.

Do not create or use a different repository.

---

## 11. Push the Project

After verifying:

- Correct branch
- Correct remote
- Correct staged files
- No secrets
- Initial commit exists

Push using:

git push -u origin main

---

## 12. Verify the Push

After pushing, verify that the push completed successfully.

Confirm:

- Local branch is main
- Remote repository is correct
- Initial commit exists
- Project files were pushed
- .env was NOT pushed
- Credentials were NOT pushed
- Authentication/storage-state files were NOT pushed
- node_modules was NOT pushed
- Test reports/results were NOT pushed

---

## Important Rules

1. Do not expose passwords, tokens, API keys, or secrets.
2. Never commit .env.
3. Never commit authentication or storage-state files.
4. Never commit node_modules.
5. Never commit generated test results or reports.
6. Do not blindly use git add .
7. Review untracked files before staging.
8. Do not modify Salesforce automation code during this phase.
9. Do not generate framework implementation code during this phase.
10. If an unexpected sensitive file is found, stop and request human approval.
11. Do not push until the staging area has been reviewed.

---

## Final Report

After completing this phase, provide:

1. Current branch
2. GitHub remote
3. Files committed
4. Files intentionally excluded
5. Files requiring human approval
6. Confirmation that .env was not committed
7. Confirmation that no secrets were committed
8. Confirmation that authentication/storage-state files were not committed
9. Push status

This phase is complete only when the existing project has been safely pushed to the correct public GitHub repository.

Do NOT proceed to Salesforce framework implementation from this prompt.