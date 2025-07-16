# LLM Cloud-Agnostic K8s Terraform

Cloud-agnostic, Terraform-driven deployment of Large Language Model (LLM) serving and inference on Kubernetes (GKE, EKS, or AKS).

## Overview

This project provides a template and automation scripts for deploying a LLM (Large Language Model) inference server to your choice of a managed Kubernetes cluster (GKE, EKS, or AKS) using Terraform. The stack is portable: you choose your cloud platform, and the setup process remains the same.

## Features

- **Cloud-agnostic:** Deploy on Google Kubernetes Engine (GKE), Amazon Elastic Kubernetes Service (EKS), or Azure Kubernetes Service (AKS)
- **Terraform Infrastructure-as-Code:** All resources and configurations are defined in version-controlled Terraform files
- **Kubernetes-native:** Model server runs as a containerized service with scalable deployment and secure networking
- **Easy Customization:** Adjust model, hardware requirements, and environment with minimal changes
- **Open-Source Model Support:** Start with Llama-2 7B or swap in any open-access model

## Quick Start

### Prerequisites

- GitHub account
- Terraform CLI and a compatible cloud CLI (gcloud, aws, or az)
- Access to GKE, EKS, or AKS (cloud account with sufficient permissions)
- kubectl

### Deployment Steps

1. **Clone the Repository**
   ```bash
   git clone https://github.com/sanskargupta551/llm-cloud-agnostic-k8s-terraform.git
   cd llm-cloud-agnostic-k8s-terraform
   ```

2. **Configure Terraform**
   - Edit `main.tf` and `variables.tf` to select your cloud provider and region.
   - Supply your cloud credentials as environment variables or configuration.

3. **Initialize and Apply**
   ```bash
   terraform init
   terraform plan
   terraform apply
   ```

4. **Access Your LLM Server**
   - After deployment, follow onscreen instructions or check the output for endpoint access details.
   - Use `kubectl` to inspect deployments or troubleshoot.

## Directory Structure

```
llm-cloud-agnostic-k8s-terraform/
│
├── README.md                 # Project overview, instructions, badges
├── LICENSE                   # MIT License (or as chosen)
├── .gitignore                # Ignore system/build files
│
├── terraform/                # All IaC code and environments
│   ├── main.tf               # Main Terraform configuration
│   ├── variables.tf          # Input variables
│   ├── outputs.tf            # Exported outputs
│   ├── providers.tf          # Cloud provider initialization (GCP, AWS, Azure)
│   ├── versions.tf           # Terraform and provider constraints
│   ├── modules/              # Optional: custom or shared Terraform modules
│   └── environments/         # (Optional) env-specific configs (dev, prod, etc.)
│
├── k8s/                      # Kubernetes deployment manifests
│   ├── deployment.yaml       # LLM serving Deployment spec
│   ├── service.yaml          # Kubernetes Service for model endpoint
│   ├── ingress.yaml          # (Optional) Ingress or Gateway setup
│   ├── configmap.yaml        # (Optional) Model/config data
│   └── hpa.yaml              # (Optional) Horizontal pod autoscaling
│
├── scripts/                  # Automation and helper scripts (shell, python, etc.)
│   ├── deploy.sh             # End-to-end deployment helper
│   ├── destroy.sh            # Tear down infrastructure
│   └── validate.sh           # Pre-flight checks
│
├── model/                    # (Optional) Model assets/configs
│   └── README.md             # Notes on model selection, links, config tips
│
├── docs/                     # Documentation: design diagrams, guides, etc.
│   ├── overview.md
│   ├── architecture.png
│   └── howto-infer.md
│
└── assets/                   # Images, logos, diagrams
    └── llm-diagram.png
```

## Supported Models

- Llama-2 7B (default)
- Swap in any open-weights model by adjusting container image or scripts.

## License

This project is licensed under the **MIT License**.  
You are free to use, modify, and distribute with attribution.

## Contributing

Contributions, issues, and discussions are welcome! Please open an issue or submit a pull request for suggestions or improvements.

## Acknowledgements

- Meta AI (Llama-2)
- Terraform, Kubernetes, and cloud providers GCP/AWS/Azure
- Open-source ML and infra communities

*Build your own portable, cloud-agnostic LLM inference stack—learn, customize, and deploy on your favorite cloud with just a few commands!*
