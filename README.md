# Prompt Engineering on Real-World Scenarios

This repository contains separate, ready-to-use Markdown files for all 13 tasks in the UST Prompt Engineering assignment.

## Repository structure

```text
prompt-engineering-assignment/
├── README.md
├── prompts/
│   ├── Q01-messy-client-problem.md
│   ├── Q02-healthcare-risk.md
│   ├── Q03-prompt-injection.md
│   ├── Q04-toxic-biased-input.md
│   ├── Q05-financial-fraud-detection.md
│   ├── Q06-strategy-under-uncertainty.md
│   ├── Q07-complaint-classification.md
│   ├── Q08-executive-ready-output.md
│   ├── Q09-dual-audience-output.md
│   ├── Q10-self-improving-prompt.md
│   ├── Q11-prompt-evaluation-framework.md
│   ├── Q12-model-error-recovery.md
│   └── Q13-consulting-assistant-strategy.md
└── .gitignore
```

## What each task includes

Each task file contains:
1. A complete prompt that can be copied and used.
2. The recommended prompting technique and why it is suitable.
3. The reason for the prompt structure.
4. Failure modes and safeguards.
5. At least one alternative prompt design.

## Add the files to Git

After extracting the ZIP file, open a terminal in the project folder and run:

```bash
git init
git add .
git commit -m "Add prompt engineering assignment tasks"
```

To connect an existing remote repository:

```bash
git branch -M main
git remote add origin <YOUR_REPOSITORY_URL>
git push -u origin main
```

Replace `<YOUR_REPOSITORY_URL>` with your actual Git repository URL. If the repository is already initialized, do not run `git init` again.
