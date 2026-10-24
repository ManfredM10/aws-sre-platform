# Learning log

## Week 1 — IAM + VPC
- **Built:** VPC with 2 public + 2 private subnets across 2 AZs, IGW, public route table, SG. All via AWS CLI.
- **Predicted / confirmed:** public instance reaches internet (OK), private does not (FAIL).
- **Broke:** exposed an access key in a screenshot → rotated it via CLI without printing the secret.
- **Incident:** `UnauthorizedOperation` on ec2:DescribeVpcs as admin. Hypotheses: region SCP / EC2-wide SCP / legacy config.
  Tested 7 regions → only us-east-2 allowed. Root cause: org SCP restricting regions.
- **Understood:** public = route to IGW + public IP. SG remembers connections (stateful).
  Keys answer *who*; routes answer *where*. Explicit deny always wins.

## Week 2 — prep
- **Secret found in a public repo:** Slack webhook URL hardcoded in alertmanager config (restaurant-simulation-API).
  Revoked it in Slack (the step that actually closes it — it remains in git history), replaced it with a placeholder,
  untracked a committed venv. Lesson: secrets come from a secret store or env var (Alertmanager supports `api_url_file`), never the repo.
