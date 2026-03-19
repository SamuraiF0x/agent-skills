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

Publish workflow (new skill or update):

```bash
# Create or update a skill file
npx skills init skills/<skill-name>

# Commit and publish changes
git add README.md skills/<skill-name>/SKILL.md
git commit -m "feat: add or update <skill-name> skill"
git push origin main
```

Verify it is published:

- Repo skills directory:
	https://github.com/SamuraiF0x/agent-skills/tree/main/skills
- Specific skill folder:
	https://github.com/SamuraiF0x/agent-skills/tree/main/skills/<skill-name>
- Raw SKILL.md URL:
	https://raw.githubusercontent.com/SamuraiF0x/agent-skills/main/skills/<skill-name>/SKILL.md

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

