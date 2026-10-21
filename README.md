# aws-sre-platform

Hands-on AWS platform built step by step while transitioning from Linux/SecOps to Cloud Engineering.
Everything is created from the CLI first, then codified with Terraform.

## Week 1 — Network foundation (us-east-2)

~~~
                 Internet
                    |
             [ Internet Gateway ]
+-------------------+----------------------------+
| VPC sre-lab 10.0.0.0/16                         |
|  us-east-2a                 us-east-2b          |
|  pub-a  10.0.1.0/24         pub-b  10.0.2.0/24  |  <- route 0.0.0.0/0 -> IGW
|  priv-a 10.0.11.0/24        priv-b 10.0.12.0/24 |  <- local route only
+-------------------------------------------------+
SG sre-lab-web: 80/443 from anywhere, 22 from admin IP only
~~~

**Experiment:** one instance per subnet type tried to reach the internet at boot.
Result: public -> OK, private -> FAIL. Confirms that internet egress requires both
a route to the IGW and a public IP.

**Lessons:** IAM roles over long-lived keys; SG is stateful, NACL is not;
an explicit Deny in an SCP overrides AdministratorAccess (diagnosed a region-restriction SCP).
