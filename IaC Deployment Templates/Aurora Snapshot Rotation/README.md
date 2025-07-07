# Aurora Cluster Automation – Scheduled Restore & Delete (CloudFormation)

This CloudFormation template provisions an event-driven automation system to **restore** an Amazon Aurora cluster from a snapshot at a scheduled time, and **delete** it at another scheduled time using AWS Lambda and EventBridge.

It’s designed to reduce costs by ensuring Aurora clusters only run when needed — ideal for non-production, test, or training environments.

## What It Does

- Creates **two AWS Lambda functions**:
  - One to **restore** a cluster from a snapshot
  - One to **delete** the cluster automatically
- Schedules both functions to run daily using **Amazon EventBridge**
- Grants necessary **IAM permissions** to manage RDS resources
- Passes environment variables securely to the Lambda functions
- Accepts inputs for custom identifiers, security group, and subnet group

## Tech Stack

- AWS Lambda (Python 3.11)
- Amazon RDS (Aurora MySQL-compatible)
- Amazon EventBridge (for scheduling)
- AWS IAM
- AWS CloudFormation (YAML)

## Parameters

| Name                 | Type   | Description                                                              |
|----------------------|--------|--------------------------------------------------------------------------|
| `VPCSecurityGroup`   | String | The security group ID used by the restored Aurora cluster                |
| `DBSubnetGroup`      | String | The DB subnet group name for cluster networking                          |
| `SnapshotIdentifier` | String | The name or ARN of the snapshot used to restore the Aurora cluster       |
| `DBClusterIdentifier`| String | The name to assign to the restored Aurora cluster                        |

## Scheduled Times (UTC)

| Action   | Time (UTC) | Time (PDT)        |
|----------|------------|-------------------|
| Restore  | 18:00 UTC  | 11:00 AM PDT      |
| Delete   | 06:00 UTC  | 11:00 PM PDT (Previous Day) |

> You can change the cron expressions in the `ScheduleExpression` fields to adjust timing.

## Notes
- Make sure the provided snapshot exists in the same region and account.
- The cluster is restored with default settings — modify the Lambda logic if you need to attach readers, parameters, or scaling configurations.
- The deletion skips final snapshots and removes automated backups by default.

## Security Considerations
- This template grants wide permissions (Resource: "*") to RDS actions for simplicity. In production, these should be scoped to specific ARNs.
- Logs are written to CloudWatch for both Lambda functions.

## Customization Ideas
- Integrate SSM Parameter Store to dynamically pass snapshot IDs or cluster names
- Add email or SNS notification on failure/success
- Restrict SSH or modify security group permissions for more control