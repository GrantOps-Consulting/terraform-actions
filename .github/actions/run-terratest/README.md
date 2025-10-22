## run-terratest (composite action)

Installs Go + Terraform, optionally assumes an AWS role, and runs Terratests via `gotestsum`. Publishes a summary and JSON report paths as outputs.

Inputs
- `go_version` (string, default `1.23.6`)
- `terraform_version` (string, default `1.8.5`)
- `working_directory` (string, default `test`): Directory containing `go.mod` and tests.
- `test_pattern` (string, default `all`): Regex for a single test; `all` runs the whole suite.
- `timeout` (string, default `20m`)
- `aws_role_to_assume` (string, optional): Role ARN to assume.
- `aws_region` (string, default `eu-west-1`)
- `aws_session_name` (string, default `github-actions`)

Outputs
- `summary_path`: Path to the text summary file.
- `report_path`: Path to the JSON report file.

Usage
```yaml
- uses: GrantOps-Consulting/terraform-actions/.github/actions/run-terratest@v1
  with:
    go_version: 1.23.6
    terraform_version: 1.8.5
    working_directory: test
    test_pattern: TestRoute53Module_BasicRecords
    timeout: 20m
    aws_role_to_assume: arn:aws:iam::123456789012:role/ims-terraform-infrastructure-role-sandbox
    aws_region: eu-west-1
```

Notes
- Combine with the reusable Terratest workflow to run a matrix across multiple tests.
