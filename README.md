# ☁️ CloudFormation Templates by Lechu

Welcome to my collection of AWS CloudFormation templates! 🚀 This repository contains production-ready templates for various AWS services and infrastructure patterns.

## 📋 Table of Contents

- [🔐 Security Templates](#-security-templates)
- [🌐 Networking Templates](#-networking-templates)
- [⚡ Lambda & Automation Templates](#-lambda--automation-templates)
- [🚀 Quick Start](#-quick-start)
- [📖 Usage Examples](#-usage-examples)
- [🤝 Contributing](#-contributing)
- [📄 License](#-license)

## 🔐 Security Templates

### AWS Security Hub
**File:** `EnableAWSSecurityHub.yaml`

Enables AWS Security Hub with multiple security standards for comprehensive security monitoring.

**Features:**
- ✅ Enables AWS Security Hub
- 🛡️ CIS AWS Foundations Benchmark v1.4.0
- 📊 NIST 800-53 Rev 5 compliance
- 💳 PCI DSS v3.2.1 standards

**Use Case:** Perfect for organizations requiring comprehensive security compliance and monitoring across multiple frameworks.

### Amazon GuardDuty
**File:** `EnableAmazonGuardDuty.yaml`

Activates Amazon GuardDuty for intelligent threat detection.

**Features:**
- 🔍 Enables GuardDuty detector
- 📦 S3 protection enabled
- 🤖 Machine learning-based threat detection

**Use Case:** Essential for automated threat detection and security monitoring in your AWS environment.

### AWS Config
**File:** `EnableAWSConfig.yml`

Comprehensive AWS Config setup with customizable recording and delivery options.

**Features:**
- 📝 Configurable resource recording (all or specific types)
- 📧 SNS notifications support
- ⏰ Flexible snapshot delivery frequency (1h to 24h)
- 🌍 Global resource type recording option
- 📊 Compliance monitoring and configuration history

**Parameters:**
- Resource recording scope
- Delivery channel configuration
- Notification settings

**Use Case:** Ideal for compliance monitoring, configuration change tracking, and governance.

## 🌐 Networking Templates

### VPC Standard Security Groups
**File:** `vpc-standards-sg.json`

Creates standardized security groups for web applications.

**Features:**
- 🌐 WEB security group with standard ports:
  - HTTP (80)
  - HTTPS (443)
  - Alternative HTTP (8080)
  - Alternative HTTPS (8443)
- 🔒 Properly configured ingress rules
- 📋 CloudFormation Designer metadata included

**Use Case:** Standard security group for web-facing applications and load balancers.

### Multi-AZ VPC Templates
**Files:** 
- `aws-vpc.template.json` (10.0.0.0/16)
- `aws-vpc.10.0.0.0-template.json` (10.0.0.0/16)
- `aws-vpc.10.1.0.0-template.json` (10.1.0.0/16)
- `aws-vpc.10.2.0.0-template.json` (10.2.0.0/16)
- `aws-vpc.10.3.0.0-template.json` (10.3.0.0/16)
- `aws-vpc.10.21.0.0-template.json` (10.21.0.0/16)

Production-ready VPC templates with different CIDR ranges for various environments.

**Features:**
- 🏗️ Multi-AZ architecture (2-4 AZs)
- 🌐 Public and private subnets
- 🔄 NAT Gateways (or NAT instances in unsupported regions)
- 🛡️ Network ACLs for additional security
- 🏷️ Customizable subnet tagging
- ⚙️ Configurable tenancy (default/dedicated)
- 📊 Comprehensive outputs for cross-stack references

**CIDR Configurations:**
- **10.0.0.0/16** - Default/Development environment
- **10.1.0.0/16** - Testing environment
- **10.2.0.0/16** - Staging environment
- **10.3.0.0/16** - Production environment
- **10.21.0.0/16** - Special/Isolated environment

**Use Case:** Enterprise-grade VPC setup for different environments with proper network segmentation.

## ⚡ Lambda & Automation Templates

### VPN Health Check Lambda
**File:** `check-vpn-on-EC2.json`

Lambda function to monitor and restart VPN connections on EC2 instances.

**Features:**
- 🔍 Automated VPN connectivity testing
- 🔄 Automatic VPN service restart capability
- 🖥️ EC2 instance management permissions
- ⚙️ Configurable test parameters (IP, port, commands)
- 🛡️ IAM role with minimal required permissions

**Parameters:**
- Target EC2 instance ID
- VPN test IP and port
- VPN restart command
- Test command configuration

**Use Case:** Automated monitoring and healing of VPN connections in hybrid cloud environments.

### EventBridge Lambda Scheduler
**File:** `trigger-lambda-by-cron.json`

Creates EventBridge rules to trigger existing Lambda functions on a schedule.

**Features:**
- ⏰ Flexible scheduling options:
  - Every 5 minutes
  - Every 15 minutes
  - Hourly, 6-hourly, 12-hourly
  - Daily
- 🎛️ Enable/disable rule functionality
- 🔐 Proper Lambda invoke permissions
- 📊 CloudFormation outputs for monitoring

**Use Case:** Perfect for scheduling existing Lambda functions without modifying their code.

## 🚀 Quick Start

### Prerequisites
- AWS CLI configured with appropriate permissions
- CloudFormation deployment permissions
- Basic understanding of AWS services

### Deployment Steps

1. **Clone the repository:**
```bash
git clone https://github.com/Lechu77/cf-templates.git
cd cf-templates
```

2. **Deploy a template:**
```bash
# Example: Deploy Security Hub
aws cloudformation create-stack \
  --stack-name my-security-hub \
  --template-body file://EnableAWSSecurityHub.yaml \
  --region us-east-1

# Example: Deploy VPC
aws cloudformation create-stack \
  --stack-name my-vpc \
  --template-body file://aws-vpc.10.0.0.0-template.json \
  --parameters ParameterKey=AvailabilityZones,ParameterValue="us-east-1a,us-east-1b" \
  --region us-east-1
```

3. **Monitor deployment:**
```bash
aws cloudformation describe-stacks --stack-name my-security-hub
```

## 📖 Usage Examples

### Security Setup
```bash
# Enable complete security monitoring
aws cloudformation create-stack \
  --stack-name security-foundation \
  --template-body file://EnableAWSSecurityHub.yaml

aws cloudformation create-stack \
  --stack-name threat-detection \
  --template-body file://EnableAmazonGuardDuty.yaml

aws cloudformation create-stack \
  --stack-name config-monitoring \
  --template-body file://EnableAWSConfig.yml \
  --parameters ParameterKey=NotificationEmail,ParameterValue=admin@company.com
```

### Network Infrastructure
```bash
# Deploy production VPC
aws cloudformation create-stack \
  --stack-name prod-vpc \
  --template-body file://aws-vpc.10.3.0.0-template.json \
  --parameters \
    ParameterKey=AvailabilityZones,ParameterValue="us-west-2a,us-west-2b,us-west-2c" \
    ParameterKey=NumberOfAZs,ParameterValue=3

# Add security groups
aws cloudformation create-stack \
  --stack-name web-security-groups \
  --template-body file://vpc-standards-sg.json \
  --parameters ParameterKey=VPC,ParameterValue=vpc-12345678
```

### Automation Setup
```bash
# Deploy VPN monitoring
aws cloudformation create-stack \
  --stack-name vpn-monitor \
  --template-body file://check-vpn-on-EC2.json \
  --parameters \
    ParameterKey=EC2InstanceId,ParameterValue=i-1234567890abcdef0 \
    ParameterKey=TargetIP,ParameterValue=10.0.1.100 \
  --capabilities CAPABILITY_IAM

# Schedule the function
aws cloudformation create-stack \
  --stack-name vpn-scheduler \
  --template-body file://trigger-lambda-by-cron.json \
  --parameters \
    ParameterKey=LambdaFunctionName,ParameterValue=check-vpn-on-EC2 \
    ParameterKey=SchedulePeriod,ParameterValue="rate(15 minutes)"
```

## 🏗️ Template Categories

| Category | Templates | Purpose |
|----------|-----------|---------|
| **Security** 🔐 | Security Hub, GuardDuty, Config | Compliance & monitoring |
| **Networking** 🌐 | VPC variants, Security Groups | Infrastructure foundation |
| **Automation** ⚡ | Lambda functions, EventBridge | Operational automation |

## 🎯 Best Practices

- 📝 Always review parameters before deployment
- 🏷️ Use consistent naming conventions
- 🔒 Follow principle of least privilege for IAM roles
- 📊 Monitor CloudFormation events during deployment
- 🧪 Test in non-production environments first
- 💾 Keep templates in version control

## 🤝 Contributing

Contributions are welcome! Please:

1. 🍴 Fork the repository
2. 🌿 Create a feature branch
3. ✅ Test your templates thoroughly
4. 📝 Update documentation
5. 🔄 Submit a pull request

## 📄 License

This project is licensed under the terms included in the `LICENSE` file.

## 📞 Support

For questions or issues:
- 🐛 Open an issue in this repository
- 📧 Contact: [Your contact information]

---

**⭐ If you find these templates useful, please give this repository a star!**

*Made with ❤️ by Lechu*
