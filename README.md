# Terraform GitHub Actions

This repository contains a collection of GitHub Actions workflows designed to automate various Terraform operations. These workflows can be used to manage infrastructure as code (IaC) within GitHub repositories.

## Contents

- `.github/workflows/terraform-plan.yml`: This workflow performs a Terraform plan operation to show what changes would be made to your infrastructure without applying them.
- `.github/workflows/terraform-apply.yml`: This workflow applies the changes proposed in the Terraform plan to your infrastructure.
- `.github/workflows/terraform-destroy.yml`: This workflow destroys the Terraform-managed infrastructure.

## Context and Purpose

- `terraform-plan.yml` is used for previewing infrastructure changes. It's particularly useful in pull requests to ensure changes are as expected before merging.
- `terraform-apply.yml` is used to apply changes to the infrastructure after a pull request has been merged or on a specific trigger, such as a push to the main branch.
- `terraform-destroy.yml` is used to clean up resources that are no longer needed, ensuring that you're not paying for unused services.

## Implementing Workflows in Other Repositories

To implement these workflows in other repositories, follow these steps:

1. Use the reusable workflows by referencing them in your workflow file within the same organization. For example:
   ```yaml
   jobs:
     terraform:
       uses: LuckyDucky583/terraform-github-actions/.github/workflows/.terraform-aws-merge.yml@v1.1.1
       with:
         working-directory: ./terraform
       secrets: inherit
   ```
   **Note:** The workflow repository must be in the same organization as the repository using the reusable workflows.
   
2. If necessary, customize the `working-directory` or any other parameters to suit your repository's structure.
3. Ensure that your repository has the necessary secrets configured, such as `AWS_ACCESS_KEY_ID` and `AWS_SECRET_ACCESS_KEY` for AWS authentication.
4. Commit and push the changes to your repository. GitHub Actions will pick up the new workflows and run them according to their triggers.

## Prerequisites

Before using these workflows, make sure you have:

- A GitHub repository with Terraform configuration files.
- Configured secrets for cloud provider authentication.
- Reviewed the workflows to match your repository's branching strategy and Terraform version.

For more detailed instructions and troubleshooting, refer to the individual workflow files within this repository.
