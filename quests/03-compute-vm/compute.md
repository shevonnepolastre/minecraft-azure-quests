## Project Overview

Automated pipeline to deploy a Minecraft server on an Ubuntu VM in Azure, built with Bicep and GitHub Actions. The scenario is a framing device — the goal was to understand how Azure infrastructure actually fits together and how to build it with code rather than clicking through the portal.

---

## Key Concepts Covered

- Azure Bicep (Infrastructure as Code)
- GitHub Actions — linting, Azure CLI, Bash scripting
- YAML syntax and structure
- SSH keys for secure VM authentication
- PowerShell basics
- User-assigned managed identities
- Virtual networks and subnets
- Network security groups (NSGs)

---

## What I Built and Learned

- Writing YAML for GitHub workflows
- Automating deployments with CI/CD pipelines
- Configuring and running a GitHub Actions runner
- Managing SSH keys for Azure VMs
- Writing Bicep templates and modules from scratch
- Troubleshooting ARM/Bicep template errors and pipeline failures
- Debugging CI/CD issues in real time
- Understanding how Azure VMs, networking, and identity components connect

---

## Reference Resources

- [Quickstart: Create an Ubuntu Linux VM using a Bicep file](https://learn.microsoft.com/en-us/azure/virtual-machines/linux/quick-create-bicep?tabs=CLI)
- [Deploy a free private Minecraft server with Azure for Students](https://techcommunity.microsoft.com/blog/educatordeveloperblog/how-to-deploy-your-free-private-minecraft-server-with-azure-for-student/3693328)
- [A Cloud Guru: GitHub Actions Deep Dive](https://learn.acloud.guru/course/github-actions-deep-dive/dashboard)
