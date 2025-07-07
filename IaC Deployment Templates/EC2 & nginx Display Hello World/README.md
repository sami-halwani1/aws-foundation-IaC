# EC2 Hello World with NGINX – CloudFormation Template

This CloudFormation template provisions an Amazon EC2 instance running NGINX, pre-configured to display a simple "Hello, World" message. It also sets up a security group allowing HTTP and SSH access.

## What It Does

- Launches a **t2.micro** EC2 instance using the **Amazon Linux 2023 AMI**
- Installs and starts **NGINX** via EC2 UserData
- Creates a basic HTML page at the root web directory
- Configures a **security group** that allows inbound HTTP (port 80) and SSH (port 22)
- Outputs the **public IP address** of the instance

## Tech Stack

- AWS EC2
- NGINX
- Amazon Linux 2023
- AWS CloudFormation (YAML)

## Parameters

| Name      | Type   | Description                                        |
|-----------|--------|----------------------------------------------------|
| `KeyName` | String | Name of an existing EC2 KeyPair to allow SSH access|

> **Note:** Make sure the specified KeyPair already exists in your AWS region before deploying.

## Output

| Name       | Description                               |
| ---------- | ----------------------------------------- |
| `PublicIP` | The public IP address of the EC2 instance |

## Accessing the Instance
- Once deployed, note the PublicIP output.
- Visit http://<PublicIP> in your browser to see the "Hello, World" message.
- To SSH into the instance:
```bash
ssh -i /path/to/your-key.pem ec2-user@<PublicIP>
```
## Security Considerations
- Port 22 (SSH) is open to the world (0.0.0.0/0). You should restrict this in production.
- The instance uses a public IP and is internet-accessible by default.


