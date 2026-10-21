# Week 1 commands (summary)
1. `aws ec2 create-vpc` + `modify-vpc-attribute --enable-dns-hostnames`
2. 4 × `create-subnet` (2 AZs), `modify-subnet-attribute --map-public-ip-on-launch` on public ones
3. `create-internet-gateway` + `attach-internet-gateway`
4. `create-route-table`, `create-route 0.0.0.0/0 → IGW`, `associate-route-table` (public only)
5. `create-security-group` + `authorize-security-group-ingress`
6. 2 × `run-instances` with user-data connectivity test, read via `get-console-output`, then `terminate-instances`
Next week this becomes Terraform.
