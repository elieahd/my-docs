[GitHub CLI](https://cli.github.com/) brings GitHub to your terminal.

Here are some commands that you can try

### View Repo

```shell
gh repo view ${REPO}
```

This will allow you to see the repository description & `README.md` 

**Example** : View `elieahd/blogger-hexagonal`

```shell
gh repo view elieahd/blogger-hexagonal
```

![view repo](../../assets/gh-cli/view-repo.png)

### Workflows

```shell
gh workflow list --repo ${REPO}
```

**Example** : List workflows of the repo `elieahd/blogger-hexagonal`

```shell
gh workflow list --repo elieahd/blogger-hexagonal
```

![workflow list](../../assets/gh-cli/workflow-list.png)

**Example** : List workflows of the repo `elieahd/blogger-hexagonal` with formatted JSON output

```shell
gh workflow list --repo elieahd/blogger-hexagonal --json id,name
```

![workflow list json](../../assets/gh-cli/workflow-list-json.png)
todo

**Example** : List workflows name of the repo `elieahd/blogger-hexagonal` 

```shell
gh workflow list --repo elieahd/blogger-hexagonal --json id,name -q '.[].name'
```

![workflow list name](../../assets/gh-cli/workflow-list-name.png)

### Runs

```shell
gh run list --repo ${REPO} --workflow ${WORKFLOW}
```

**Example** : List workflows runs of `Dependabot Updates` in the repo `elieahd/blogger-hexagonal`

```shell
gh run list --repo elieahd/blogger-hexagonal --workflow 'Dependabot Updates'
```

![workflow runs](../../assets/gh-cli/workflow-runs.png)

### Pull Requests

```shell
gh pr list --repo ${REPO} --state open
```

**Example** : List all opened PRs on `elieahd/blogger-hexagonal`

```shell
gh pr list --repo elieahd/blogger-hexagonal --state open
```

![opened prs](../../assets/gh-cli/prs-opened.png)

**Example** : List all assigned PRs on `elieahd/blogger-hexagonal`

```shell
gh pr status --repo elieahd/blogger-hexagonal 
```

![assigned prs](../../assets/gh-cli/assigned-prs.png)

### Checks on PRs

```shell
gh pr checks ${PR} --repo ${REPO}
```

**Example** : List all checks on a specific PR on `elieahd/blogger-hexagonal`

```shell
gh pr checks 12 --repo elieahd/blogger-hexagonal
```

![pr cheks](../../assets/gh-cli/pr-checks.png)


Here is the full list of [commands](https://cli.github.com/manual)
