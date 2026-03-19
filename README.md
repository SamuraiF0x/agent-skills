# Agent Skills

Personal agent skills for installation via npx skills add.

## Included skills

- refactor: Refactor existing code with strict behavior parity.
- improve-arch: Follow-up to refactor for deep-module architecture improvements.

## Create New Skill

Run init in the target folder so the template is created where you want it:

```bash
npx skills init skills/my-new-skill
```

## Publish

GitHub repository:
https://github.com/SamuraiF0x/agent-skills

Install from published sources:

```bash
npx skills add samuraif0x/agent-skills
npx skills add https://github.com/SamuraiF0x/agent-skills
npx skills add https://github.com/SamuraiF0x/agent-skills/tree/main/skills/refactor
npx skills add https://github.com/SamuraiF0x/agent-skills/tree/main/skills/improve-arch
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

