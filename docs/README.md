# Project Summary: **llm-cloud-agnostic-k8s-terraform**

## Overview

**llm-cloud-agnostic-k8s-terraform** is a modern MLOps portfolio project that enables users to provision, serve, and interact with large language models (LLMs) using Kubernetes clusters on any major public cloud—Google Cloud (GKE), AWS (EKS), or Azure (AKS)—all via automated and reproducible Terraform Infrastructure-as-Code. The project features a powerful, interactive local Streamlit web client, robust security and DevOps practices, and a multi-layered cleanup strategy to ensure cost control and sustainability.

## Key Features

- **Multi-Cloud Support:**  
  Deploy the full LLM serving stack with GPU-enabled Kubernetes clusters on GCP, AWS, or Azure using cloud-native services and resources.

- **End-to-End Automation:**  
  One-click Terraform deployment for each cloud. Automatic provisioning of Kubernetes clusters, node pools, networking, artifacts, secrets, monitoring, and LLM API endpoints.

- **Dynamic LLM Model Selection:**  
  At app launch, fetch and list all compliant public LLMs from HuggingFace in a dropdown menu for real-time model deployment and testing.

- **Interactive & Persistent Chat UI:**  
  Local Streamlit application provides a user-friendly chat interface with context retained throughout each chat session until reset or model switch.

- **Flexible, Reliable Cleanup:**  
  Three distinct methods for guaranteed resource cleanup (see details below).

- **Security & Best Practice:**  
  Uses secret managers, least-privilege IAM, cloud-native container/image registry, private networking, and cloud-native monitoring/logging.

## Architecture

### Main Components
- **Kubernetes Cluster (GKE/EKS/AKS):** Robust, autoscaled, GPU-enabled cluster for LLM inference.
- **LLM Inference API with Model Deployment:** Exposes `/deploy_model` and `/generate` endpoints, managing lifecycle and serving of user-selected models.
- **Cloud-Native Artifact, Secret, and Object Storage:** Integrates with the registry, secret manager, and storage services native to each cloud.
- **Streamlit Web Client (Local):** Connects securely to the deployed inference service, handling model management and chat.

### Project Structure

```
llm-cloud-agnostic-k8s-terraform/
│
├── deployments/
│   ├── gcp/                       # Terraform configs and scripts for Google Cloud (GKE)
│   │   ├── main.tf
│   │   ├── variables.tf
│   │   ├── outputs.tf
│   │   ├── terraform.tfvars.example
│   │   ├── cleanup.sh             # Cleanup script for GCP
│   │   └── README.md              # GCP-specific deployment and cleanup instructions
│   │
│   ├── aws/                       # Terraform configs and scripts for AWS (EKS)
│   │   ├── main.tf
│   │   ├── variables.tf
│   │   ├── outputs.tf
│   │   ├── terraform.tfvars.example
│   │   ├── cleanup.sh             # Cleanup script for AWS
│   │   └── README.md              # AWS-specific deployment and cleanup instructions
│   │
│   └── azure/                     # Terraform configs and scripts for Azure (AKS)
│       ├── main.tf
│       ├── variables.tf
│       ├── outputs.tf
│       ├── terraform.tfvars.example
│       ├── cleanup.sh             # Cleanup script for Azure
│       └── README.md              # Azure-specific deployment and cleanup instructions
│
├── streamlit_app/                 # Local Streamlit web client code (frontend)
│   ├── app.py                     # Main Streamlit app entrypoint
│   ├── requirements.txt           # Python dependencies for frontend
│   ├── utils.py                   # Utility functions (e.g., HuggingFace API calls)
│   └── README.md                  # Usage and run instructions for the Streamlit app
│
├── api_backend/                   # Optional: Backend API service (e.g., FastAPI) if separated from frontend
│   ├── main.py                    # API backend server code
│   ├── requirements.txt
│   └── README.md
│
├── docs/                          # Documentation files
│   ├── architecture.md            # System design and architecture overview
│   ├── usage.md                   # Detailed user guide and workflow
│   ├── security.md                # Security and best practices details
│   └── troubleshooting.md         # Common issues and resolutions
│
├── .gitignore                     # Git ignore patterns
├── LICENSE                        # License file (e.g., MIT)
└── README.md                      # Project summary, quickstart, and overview for GitHub
```

## Typical User Flow

1. **Prepare Cloud Credentials:** User configures authentication for preferred cloud platform.
2. **Provision Resources via Terraform:** User runs deployment script for chosen cloud.
   - **Automated:** Resources are provisioned, local Streamlit client launches and connects, all available LLMs are fetched and listed.
3. **Deploy Desired LLM:** User selects an LLM from the dropdown and deploys it (removes previous, if any).
4. **Chat with Model:** Interact via chat interface with full context retention.
5. **Reset or Switch Model:** Reset chat context or swap to a different LLM as needed.
6. **Resource Cleanup:** Use any of the three cleanup options (see below).

## Multi-Layered Resource Cleanup

**All resources are cleaned using one (or more) of these approaches:**

1. **Automatic Idle Timeout:**  
   System continuously monitors for inactivity; if no usage/activity for a defined period, all cloud resources are auto-destroyed.

2. **Manual In-App Cleanup Button:**  
   Prominently placed "Clean-up Resources" button in the Streamlit UI allows 1-click, confirmed teardown of all provisioned infrastructure.

3. **Manual Cleanup Scripts:**  
   Ready-to-run cleanup scripts included for all cloud providers, with full documentation and command examples, for manual or emergency teardown.

## Benefits

- **Ease of Use:**  
  Minimal steps for users—just credentials, a single deployment command, and immediate app access.

- **Cloud-Native & Secure:**  
  Demonstrates modern, platform-agnostic infrastructure and MLOps deployment practices.

- **Cost-Controlled:**  
  Triple-method resource cleanup virtually eliminates "forgotten" resource costs.

- **Portfolio-Ready:**  
  Realistic, production-like workflow and engineering rigor for employer review and technical interviews.

## Documentation & Support

- Each cloud deployment folder includes usage and cleanup instructions.
- The main documentation clearly explains architecture, setup, app usage, and resource management expectations.
- Prominent cost and resource usage warnings help prevent accidental overspend.

## Summary Table

| Capability             | GCP (GKE)   | AWS (EKS) | Azure (AKS) |
|------------------------|-------------|-----------|-------------|
| Managed K8s Cluster    | ✅          | ✅        | ✅          |
| GPU Support            | ✅          | ✅        | ✅          |
| Native Container Registry | ✅       | ✅        | ✅          |
| Secrets & IAM          | ✅          | ✅        | ✅          |
| Logging/Monitoring     | ✅          | ✅        | ✅          |
| Cloud Storage          | ✅          | ✅        | ✅          |

## Final Note

**llm-cloud-agnostic-k8s-terraform** is a demonstration-ready, cloud-agnostic, cost-conscious project that showcases real-world MLOps engineering, automation, and operational best practices—ideal for portfolio presentation and technical review.