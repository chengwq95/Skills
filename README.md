# Wei Quan's Agent Skills

A growing personal collection of reusable skills for AI agents.

Skills are self-contained folders of instructions, scripts, and resources that teach an agent how to complete a specialised task reliably. This repository uses a capability-based style: a skill may work with Claude, Codex, or another capable agent without requiring a particular vendor or browser extension.

## Skills

| Skill | Description | Source | Package |
| --- | --- | --- | --- |
| E-commerce Price Compare | Evidence-backed comparison of exact product variants across marketplaces, with delivery, currency, seller, and availability checks. | [Source](./skills/ecommerce-price-compare/) | [Download](./ecommerce-price-compare.skill) |

## Repository layout

```text
.
├── skills/                 # Source of truth: one self-contained folder per skill
├── template/               # Starting point for a new skill
├── ecommerce-price-compare.skill
└── README.md               # This catalogue
```

## Add a new skill

1. Copy `template/` into `skills/<skill-name>/`.
2. Write a focused `SKILL.md` with only `name` and `description` in its YAML frontmatter.
3. Add scripts, references, or assets only when they make repeated work more reliable.
4. Validate the skill, package it as `<skill-name>.skill`, and add it to the table above.

## Compatibility and quality

- Keep each skill portable: describe required capabilities instead of naming a specific agent whenever possible.
- Record assumptions and evidence for tasks that depend on changing information.
- Do not fabricate browser, account, price, or file results when a required capability is unavailable.
- Test a skill before publishing it and state any meaningful limitations in its instructions.

## Disclaimer

These skills are personal, evolving tools. Review and test them in your own environment before relying on them for critical, financial, legal, medical, or production decisions.
