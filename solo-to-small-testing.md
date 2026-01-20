## Branch Rules & CI Standards

So that we can protect our work from major disruptions, this repository uses the "**Solo-to-Small-Testing**" ruleset to enforce the following:

### The "Green Build" Requirement
The rules for this repo use GitHub Actions to verify code quality.
*   **Status Checks:** You cannot merge a Pull Request until the automated tests (the `test` job) have passed.
*   **Blocks:** If the tests fail, the merge button will be disabled. please fix the errors and push again.

### Workflow
1.  **Pull Requests:** Direct pushed to main are blocked. All changes must go through a PR.
2.  **Self-Merging:** While code review is encouraged, it is not blocked by tooling. If the tests pass and you are confident in your code, you are free to merge without waiting for a human approval.

### Emergency Bypass
> [!NOTE]
> Repository administrators retain the ability to bypass these checks in emergency situations (e.g., if the CI provider is down or a critical hotfix is needed immediately).