# Agent Skills

Personal agent skills for installation via npx skills add.

## Included skills

- refactor: Refactor existing code with strict behavior parity.
- improve-arch: Follow-up to refactor for deep-module architecture improvements.

## Publish

Publish workflow (new skill or update):

```bash
# Commit and publish changes
git commit -m "feat: add or update <skill-name> skill"
git push origin main
```

## Install

```bash
npx skills add samuraif0x/agent-skills
npx skills add samuraif0x/agent-skills --skill refactor
npx skills add samuraif0x/agent-skills --skill improve-arch
```

## Update

```bash
npx skills update
```

## Create New Skill

Run init in the target folder so the template is created where you want it:

```bash
npx skills init skills/my-new-skill
```
