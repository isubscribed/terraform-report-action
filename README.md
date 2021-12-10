# Terraform Changes Report Action

Runs Plan and creates a github check that shows what will change against the given environment.  We assume you have authenticated the necessary permissions against your environment in order to access state and the resources.

## Inputs

### Required

- token
    - The default Github Token so we can create the check against this run

### Optional

- workspace
    - Which Terraform workspace to run against. Defaults to `default`
- check-name
    - What to name the check.  Defaults to `Terraform Report`
- directory
    - Where is the Terraform module located. Defaults to `terraform`
- terraform-version
    - What version of Terraform are you running. Defaults to `1.0.4`

## Outputs

No official outputs, but we create a check in yoru build that displays the Terraform Plan changes.


## Example

```
report:
    name: Report
    runs-on: ubuntu-latest
    steps:
      - name: Checkout
        uses: actions/checkout@v2
      - name: Configure AWS
        uses: aws-actions/configure-aws-credentials@v1
        with:
          aws-access-key-id: ${{ AWS STUFF }}
          aws-secret-access-key: ${{ AWS STUFF }}
          aws-region: ${{ REGION }}
      - name: Report Terraform Changes
        uses: isubscribed/teraform-report-action@main
        env:
          TF_VAR_example: ${{ env.SOMETHING }}
        with:
          workspace: dev
          token: ${{ secrets.GITHUB_TOKEN }}
          check-name: Terraform Report - (dev)
          directory: infrastructure/terraform
```
