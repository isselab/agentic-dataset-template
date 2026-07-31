# Contributing

## Using the template outside `isselab`

You do not need to belong to the `isselab` organization to use this template
or validate a dataset. Create a repository from the template in your personal
account or another organization where you have permission to create
repositories.

The bootstrap and parent-synchronization workflows are specific to `isselab`:
they require the `PARENT_REPO_PAT` secret and permission to update the official
dataset catalog. In an external repository, the first bootstrap run may
therefore fail. Do not request or substitute an organization token. Instead:

1. Remove `.github/.bootstrap`, `.github/workflows/bootstrap.yml`,
   `.github/workflows/sync-parent.yml`, and
   `.github/scripts/bootstrap_dataset.py` from your generated repository.
2. Keep `.github/workflows/validate.yml`, `scripts/validate_dataset.py`, and the
   `schema/` directory.
3. Replace the placeholder values in `dataset.json`, including the repository
   URL and creation date, and replace the template README with a description
   of your dataset.
4. Follow the authoring workflow in the README and run the validator locally
   before pushing changes:

   ```bash
   python scripts/validate_dataset.py
   ```

The retained **Validate dataset** workflow runs the same validation on every
push and pull request and does not require organization secrets.

An externally maintained dataset is not registered automatically in
`isselab/agentic-feature-traced-datasets`. Contact that repository's
maintainers separately if you want to propose it for inclusion.
