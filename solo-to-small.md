## Branch Rules & Workflow

So that we can protect our work from major disruptions, this repository uses the "**Solo-to-Small**" ruleset to enforce the following:

### The "PR First" Policy
Even for solo work or small fixes, **direct commits to the main branch are blocked.**
*   **Why?** It prevents accidental history rewrites and ensures every change—no matter how small—gets a "self-review" via a Pull Request diff.
*   **How to Merge:** Open a Pull Request. You do **not** need to wait for an approval or a code review. Once you are happy with your own changes, you can merge immediately.

These rules will automatically be applied, even for solo authors.

### History Safety
*   **No Force Pushes:** The main branch history is immutable.
*   **No Deletions:** The main branch cannot be deleted.

> [!TIP]
> If you are collaborating with others, approvals are welcome but not strictly enforced by the software. Please communicate with the team if you want a second pair of eyes before merging. Or, see `README.md` about possibly tweaking the rules.