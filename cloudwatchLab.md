## Step 1 – Launch an EC2 Instance

- Open AWS Console → EC2 → Launch Instance.
- Choose Amazon Linux 2 AMI (Free Tier).
- Instance type: t2.micro.
- Configure:
  - IAM Role: create or attach a role with CloudWatchAgentServerPolicy.
  - Network & Security: allow SSH (port 22) from your IP.
  - Storage: default 8 GB.
  - Launch and download key pair (if you don’t have one).

- Connect via SSH:
```
ssh -i mykey.pem ec2-user@<public-ip>
```

## Step 2 – Install CloudWatch Agent

- Update packages:
```
sudo yum update -y
```

- Install the agent:
```
sudo yum install -y amazon-cloudwatch-agent
```

## Step 3 – Create CloudWatch Agent Config

- Run the interactive wizard:
```
sudo /opt/aws/amazon-cloudwatch-agent/bin/amazon-cloudwatch-agent-config-wizard
```

- Wizard flow (recommended answers):

1. Collect metrics → Yes
2. Which metrics → CPU, memory, disk, network
3. Save config → Yes (default location: /opt/aws/amazon-cloudwatch-agent/bin/config.json)

4. Move config to correct path:
```
sudo cp /opt/aws/amazon-cloudwatch-agent/bin/config.json /opt/aws/amazon-cloudwatch-agent/etc/amazon-cloudwatch-agent.json
```

## Step 4 – Start CloudWatch Agent
```
sudo systemctl start amazon-cloudwatch-agent
sudo systemctl enable amazon-cloudwatch-agent
sudo systemctl status amazon-cloudwatch-agent
```


Status should be: active (running).
Check logs for errors:

```
sudo tail -f /opt/aws/amazon-cloudwatch-agent/logs/amazon-cloudwatch-agent.log
```

## Step 5 Validate
Go to cloudwatch and check for CWAgent namespace
Explore the metrics
