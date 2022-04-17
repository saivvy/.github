# Contributing to Saivvy

## GitHub Workflow

The recommended workflow is to create your own branch and open pull request once ready.

### 1. clone the repository

```sh
# Clone repository
git clone https://github.com/saivvy/$REPOSITORY.git

# Add upstream origin
git remote add upstream git@github.com:saivvy/$REPOSITORY.git
```

### 2. Create a pull request

```sh
# Create a new feature branch
git checkout -b my_feature_branch

# Make changes to your branch
# ...

# Commit changes - remember to sign!
git commit -s

# Push your new feature branch
git push my_feature_branch

# Create a new pull request from https://github.com/saivvy/$REPOSITORY
```

## Scope of pull requests

We prefer small incremental changes that can be reviewed and merged quickly.
It's OK if it takes multiple pull requests to close an issue.

The idea is that each improvement should land in saivvy's main branch within a
few hours.  The sooner we can get multiple people looking at and agreeing on a
specific change, the quicker we will have it out in a release.  The quicker we
can get these small improvementes in a Saivvy release, the quicker we can get
feedback from our users and find out what doesn't work, or what we have missed.

The added benefit is that this will force everyone to think about handling
partially implemented features & non-breaking changes. Both are great
approached, and they work really well in the context of Saivvy.


### Commit messages

[How to Write a Git Commit Message](https://chris.beams.io/posts/git-commit/)

Guidelines:

- **Group Commits:** Each commit should represent a meaningful change (e.g. implement feature X, fix bug Y, ...).
  - For instance, a PR should not look like _1) Add Feature X 2) Fix Typo 3) Changes to features X 5) Bugfix for feature X 6) Fix Linter 7) ...
  - Instead, these commits should be squashed together into a single "Add Feature" commit.
- Each commit should work on its own: it must compile, pass the linter and so on.
  - This makes life much easier when using `git log`, `git blame`, `git bisect`, etc.
  - For instance, when doing a `git blame` on a file to figure out why a change
  was introduced, it's pretty meaningless to see a _Fix linter_ commit message.
  "Add Feature X" is much more meaningful.
- Use `git rebase -i main` to group commits together and rewrite their commit message
- To add changes to the previous commit, use `git commit --amend -s`. This will
  change the last commit (amend) instead of creating a new commit.
- Format: Use the imperative mood in the subject line: "If applied, this commit
  will _your subject line here_"
- Add the following prefixes to your commit message to help trigger automated processes[^1]:
  - `docs:` for documentation changes only (e.g., `docs: Fix typo in X`);
  - `test:` for changes to tests only (e.g., `test: Check if X does Y`);
  - `chore:` general things that should be excluded (e.g., `chore: Clean up X`);
  - `website:` for the documentation website (i.e., the frontend code; e.g., `website: Add X link to navbar`);
  - `ci:` for internal CI specific changes (e.g., `ci: Enable X for tests`);
  - `infra:` for infrastructure changes (e.g., `infra: Enable cloudfront for X`);

[^1]: See [https://www.conventionalcommits.org](https://www.conventionalcommits.org)

## Docs

### Use relative links to markdown files

Link to markdown files (`[link](../foo.md)`) instead of relative URLs
(`[link](/foo)`).

The docs compiler will replace file links with relative URLs automatically.

This is to avoid broken links. If a file gets renamed, the compiler will
catch broken links and throw an error. Relative URLs get broken unnoticed.

## FAQ

### How to run the markdown linter locally

First install `markdownlint-cli`:

- On Mac OS: `brew install markdownlint-cli`
- On other systems, with yarn installed: `yarn global add markdownlint-cli`

Then from the repository root:

```console
markdownlint -c .markdownlint.yaml docs/**/*.md
```

### How to re-run all GitHub Actions jobs?

There isn't a button that Saivvy contributors can click in their fork that will
re-run all GitHub Actions jobs.

The current workaround is to re-create the last commit:

```sh
git commit --amend -s

# Force push the new commit to re-run all GitHub Actions jobs:
git push -f mybranch
```
