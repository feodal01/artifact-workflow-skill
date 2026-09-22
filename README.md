# artifact-workflow

Agent skill for creating clear, consistent, and reproducible documents, reports, and diagrams.

## Installation in Codex

Choose one installation method.

### Ask Codex to install it

Send this prompt to Codex:

```text
Use $skill-installer to install the skill from https://github.com/feodal01/artifact-workflow.
The skill is at repository path "."; install it with the name "artifact-workflow".
```

### Install manually

With Git installed, run these commands in a macOS or Linux terminal:

```sh
mkdir -p "$HOME/.agents/skills"
git clone https://github.com/feodal01/artifact-workflow.git "$HOME/.agents/skills/artifact-workflow"
```

This installs the skill for your user across projects. Keep the entire directory: `SKILL.md` uses the files in `references/`.

Codex detects installed skills automatically. If the skill does not appear, restart Codex. See the [official skill installation documentation](https://learn.chatgpt.com/docs/build-skills#install-curated-skills-for-local-use).

## Usage

Mention `$artifact-workflow` in your next Codex prompt, for example:

```text
Use $artifact-workflow to create an analytical report from the supplied data.
Answer this question: which customer segments account for the conversion decline?
```
