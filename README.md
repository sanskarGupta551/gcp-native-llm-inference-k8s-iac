# LLM Cloud-Agnostic K8s Terraform

Cloud-agnostic, Terraform-driven deployment of Large Language Model (LLM) serving and inference on Kubernetes (GKE, EKS, or AKS).

## Overview

This project provides a template and automation scripts for deploying an LLM (Large Language Model) inference server and a simple Streamlit website to your choice of a managed Kubernetes cluster (GKE, EKS, or AKS) using Terraform. The stack is portable: you choose your cloud platform, and the setup process remains the same.

## Features

- **Cloud-agnostic:** Deploy on Google Kubernetes Engine (GKE), Amazon Elastic Kubernetes Service (EKS), or Azure Kubernetes Service (AKS)
- **Terraform Infrastructure-as-Code:** All resources and configurations are defined in version-controlled Terraform files
- **Kubernetes-native:** Model server and Streamlit UI run as containerized services with scalable deployment and secure networking
- **User-Friendly Inference:** All model inferences are performed directly from the deployed Streamlit web interface
- **Easy Customization:** Adjust model, hardware requirements, and environment with minimal changes
- **Open-Source Model Support:** Start with Llama-2 7B or swap in any open-access model

## Quick Start

### Prerequisites

- GitHub account
- Terraform CLI and a compatible cloud CLI (`gcloud`, `aws`, or `az`)
- Access to GKE, EKS, or AKS (cloud account with sufficient permissions)
- `kubectl`

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

4. **Access the Streamlit Inference UI**
   - After deployment, the output will display the external URL of your Streamlit web interface.
   - Open this link in your browser.

5. **Use the Web Interface for Inference**
   - Enter your prompt or input directly in the Streamlit interface.
   - Click the "Run Inference" button to send your query to the deployed LLM model server.
   - View the model's response instantly in the browser—no additional tools or code required.

   > **Tip:** All model serving and inference is handled through the user-friendly Streamlit website, making testing and demonstration seamless.

## Directory Structure

```
llm-cloud-agnostic-k8s-terraform/
│
├── README.md                     # Project overview, instructions, badges
├── LICENSE                       # MIT License
├── .gitignore                    # Ignore system/build files and secrets
│
├── terraform/                    # All Terraform IaC code and environments
│   ├── main.tf                   # Main Terraform configuration
│   ├── variables.tf              # Input variables
│   ├── outputs.tf                # Exported outputs
│   ├── providers.tf              # Cloud provider init (GCP, AWS, Azure)
│   ├── versions.tf               # Terraform and provider constraints
│   ├── modules/                  # Optional: custom/shared Terraform modules
│   └── environments/             # (Optional) env-specific configs
│
├── k8s/                          # Kubernetes deployment manifests
│   ├── deployment.yaml           # LLM serving Deployment spec
│   ├── service.yaml              # Service for model endpoint
│   ├── streamlit.yaml            # Streamlit UI Deployment spec
│   ├── streamlit-service.yaml    # Expose Streamlit app (LoadBalancer, etc.)
│   ├── ingress.yaml              # (Optional) Ingress or Gateway
│   ├── configmap.yaml            # (Optional) Config/Secrets for apps
│   └── hpa.yaml                  # (Optional) Horizontal pod autoscaling
│
├── streamlit_app/                # Streamlit webapp source code
│   ├── app.py                    # Main Streamlit Python script
│   ├── requirements.txt          # Python dependencies for Streamlit app
│   ├── utils.py                  # (Optional) Helper functions
│   ├── huggingface_helpers.py    # (Optional) HuggingFace API utils
│   └── assets/                   # (Optional) Images or static files for web UI
│
├── model/                        # (Optional) Model assets/configs
│   └── README.md                 # Notes on model selection, links, config tips
│
├── scripts/                      # Automation and helper scripts
│   ├── deploy.sh                 # End-to-end infrastructure deploy
│   ├── destroy.sh                # Tear down all infrastructure
│   └── validate.sh               # Pre-flight checks
│
├── docs/                         # Documentation: guides, diagrams, etc.
│   ├── overview.md
│   ├── architecture.png
│   └── howto-infer.md
│
└── assets/                       # Images, logos, diagrams for documentation
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

*Build your own portable, cloud-agnostic LLM inference stack—learn, customize, and deploy on your favorite cloud with just a few commands, and perform inference directly through a simple web UI!*
