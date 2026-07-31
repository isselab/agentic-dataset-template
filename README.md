# Agentic feature-traced dataset template

Use this GitHub template to create feature-evolution datasets for Agent-HAnS.
Each generated repository contains an initial project, an ordered sequence of
prompts, the intended feature changes, and the expected traceability artifacts
after each step. The template defines dataset contents and checks their structure.

## Create a dataset repository

1. Select **Use this template → Create a new repository** and create it in
   `isselab` with a short, unique name.
2. Wait for **Bootstrap dataset repository**.
3. Review and merge the registration pull request opened in
   `isselab/agentic-feature-traced-datasets`.
4. Replace all placeholder content and construct the dataset as described
   below.

Bootstrap fills the repository name, URL, and date, generates a
dataset-specific README, and removes its one-shot files. Dataset validation and
parent synchronization remain.

Users outside the `isselab` organization can also use and validate this
template. See [CONTRIBUTING.md](CONTRIBUTING.md) for the external workflow and
the organization-specific automation that must be removed.

## Dataset contract

```text
.
├── subject/project/                 initial project given to Agent-HAnS
├── benchmark/
│   ├── steps.json                   ordered step index
│   └── steps/step-NNN/
│       ├── step.json                transition and intended feature changes
│       ├── prompts/                 exact ordered prompts
│       └── ground-truth/            expected post-step traceability artifacts
├── docs/                              dataset-specific documentation
├── schema/
├── scripts/validate_dataset.py
├── dataset.json
└── LICENSE
```

The subject is version `v000`. Each step transitions from one logical version
to the next and is executed on the working state produced by the preceding
step.

Ground truth contains the expected feature model, folder mappings, file
mappings, fragment annotations, and interactions after a step.

## Authoring workflow

1. Replace `subject/project` with the complete initial project.
2. Complete `dataset.json`, including provenance and limitations.
3. Replace `step-001` with the first controlled evolution step.
4. Preserve each prompt exactly and list multiple prompts in execution order.
5. Record intended changes using the exact feature names from the feature model.
6. Create the expected post-step traceability artifacts.
7. Copy `step-001` for later steps and update `benchmark/steps.json`.
8. Keep version transitions continuous: `v000 → v001 → v002`, and so on.

Run validation locally:

```bash
python scripts/validate_dataset.py
```

The validator checks the dataset contract, referenced files, step ordering, and
version continuity. It does not evaluate an agent's generated result.

## Automation and security

`PARENT_REPO_PAT` must be a fine-grained token restricted to the parent
repository with **Contents: read and write** and **Pull requests: read and
write**. Prefer a narrowly available organization Actions secret.

Parent changes are always proposed by pull request. Protect the parent's
`main` branch and require its catalog validation workflow.

If bootstrap runs before its secret is available, it fails without deleting
the bootstrap marker. Add the secret and rerun the job.

## License

The template is MIT-licensed. A generated dataset must state the license of
its code, prompts, and annotations in both `LICENSE` and `dataset.json`.
