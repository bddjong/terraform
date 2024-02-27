# Terraform for NL Design System

## Getting started

On macOS:

1. Install Homebrew
2. Install GitHub CLI: `brew install gh`
3. [Install Terraform](https://developer.hashicorp.com/terraform/tutorials/aws-get-started/install-cli):
4. `brew tap hashicorp/tap`
5. `brew install hashicorp/tap/terraform`

Then configure this project:

- Configure the `GH_TOKEN` environment variable with an fine-grained access token with enough rights.

## Importing an existing repo

```shell
terraform import "github_repository.terraform-playground" "name-of-github-repository-resource"
```

## Fine-grained personal access token for GitHub

The following token can be used locally to read all the current settings of your GitHub organisation, repositories, teams, et cetera.

Create the following GitHub token, and store it in `.env` as `export GITHUB_TOKEN=...`.

Resource owner: `nl-design-system`:

- Repository:
  - Administration: read and write
  - Issues: read and write (voor labels)
  - Metadata: read only
  - Pages: read and write
- Organization:
  - Administration: read only
  - Members: read and write

To create the token to actually apply all changes, you must configure a "read and write" token. This is the token you would configure in Terraform Cloud for example (recommended), or the token you would use if you would apply state from your own computer (not recommended).

## Terraform Cloud

### How to stop using cloud services

The following code is responsible for storing the Terraform state in the cloud:

```
  cloud {
    organization = "nl-design-system"

    workspaces {
      name = "github"
    }
  }
```

Removing this code should allow you to switch back to storing state in `terraform.tfstate`.

## API Documentation

- data source: [`github_organization`](https://registry.terraform.io/providers/integrations/github/latest/docs/data-sources/organization)
- provider: [`github_branch_protection`](https://registry.terraform.io/providers/integrations/github/latest/docs/resources/branch_protection)
- provider: [`github_repository_collaborators`](https://registry.terraform.io/providers/integrations/github/latest/docs/resources/repository_collaborators)
- provider: [`github_repository`](https://registry.terraform.io/providers/integrations/github/latest/docs/resources/repository)
- provider: [`github_team`](https://registry.terraform.io/providers/integrations/github/latest/docs/data-sources/team)