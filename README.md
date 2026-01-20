# Rulesets

A personal collection of GitHub repository rulesets for solo developers and small teams, like me. Inspired by the GitHub [Ruleset Recipies](https://github.com/github/ruleset-recipes) repository.

## About

This repository contains reusable GitHub ruleset configurations and corresponding `CONTRIBUTING.md` fragments that explain the rules to collaborators.

| Ruleset | Description | Best For |
|---------|-------------|----------|
| `solo-to-small.json` | PR-required workflow with no approval gates | Solo projects, experiments, personal sites |
| `solo-to-small-tests.json` | PR-required workflow with CI status checks | Projects with automated tests |

## Philosophy

These rulesets are designed around a simple idea: protect `main`, have a flow, but otherwise stay out of the way.

They enforce just enough structure to prevent accidents (force pushes, direct commits, deleted branches) without creating bureaucratic overhead for small teams. Note that for teams growing in size a first tweak might be `required_approving_review_count` from `0` to `1` or `2`.

## Usage

### Prerequisites

- [GitHub CLI](https://cli.github.com/) installed and authenticated (`gh auth login`)
- Admin access to the target repository

### Step 1: Clone this repository

```bash
gh repo clone peterdresslar/rulesets
cd rulesets
```

### Step 2: Choose your ruleset

Review the JSON files and pick the one that fits your project:

```bash
cat solo-to-small.json          # Solo or small team with no CI requirements
cat solo-to-small-tests.json    # Solo or small team requires passing tests
```

### Step 3: Apply the ruleset to your repository

Using the GitHub web interface, go to your Repo's Settings tab. Under the Rules item in the Settings nav, click "Rulesets". Click "New Ruleset" and from the dropdown select "Import a Ruleset". Navigate to the cloned repo on your desktop and select the ruleset you prefer.

**Important**: Once you import, you will see a toast message that says "This ruleset has been imported but the changes have not been saved. Review and save the changes below." You must scroll to the very bottom of the page and click the button to Save Changes to continue.

### Step 4: Verify

You can use `gh ruleset list` to inspect the added ruleset from a command line at your local repository. It should appear immediately without a `fetch` (note that `gh` is not `git`!) You can also use `gh ruleset --help` for a few more `ruleset` commands. You should see your new ruleset in the response.

### Step 5: Add the CONTRIBUTING fragment (optional)

If you like, copy the relevant `[ruleset].md` content into your project's `CONTRIBUTING.md` file so collaborators understand the rules.

## Customization

### Changing the required approval count

To require one approval before merging, edit the JSON:

```json
"required_approving_review_count": 1
```

### Changing the status check name

If your CI job isn't named `test`, update the context in `solo-tests.json`:

```json
"required_status_checks": [
    {
        "context": "your-job-name-here",
        "integration_id": 15368
    }
]
```

## Understanding Bypass Actors

The `bypass_actors` setting controls who can skip the ruleset entirely. This is useful for emergencies or workflows where the admin needs flexibility. Solo users may not need this feature at all, but we intentionally add it since a bypass actor may become relevant very quickly as the repo grows.

### How It Works

```json
"bypass_actors": [
    {
        "actor_id": 1,
        "actor_type": "RepositoryRole",
        "bypass_mode": "always"
    }
]
```

| Field | Description |
|-------|-------------|
| `actor_id` | The numeric ID of the actor. For `RepositoryRole`, `1` = Admin. For users, run `gh api user --jq '.id'` to get your ID. |
| `actor_type` | Who can bypass: `RepositoryRole`, `OrganizationAdmin`, `Team`, or `Integration` |
| `bypass_mode` | `always` = bypass anytime, `pull_request` = must still open a PR but can merge without meeting requirements |

### Common Configurations

**Let repository admins bypass everything:**
```json
{
    "actor_id": 5,
    "actor_type": "RepositoryRole",
    "bypass_mode": "always"
}
```

**Let a specific user bypass (e.g., yourself):**
```json
{
    "actor_id": 2095978,
    "actor_type": "User",
    "bypass_mode": "always"
}
```
Find your user ID with: `gh api user --jq '.id'`

*Note*: Roles vary for GitHub Pro, Team, and Enterprise users, so if you are working on one of those accounts or within an organization this setting will require a bit of extra care.


