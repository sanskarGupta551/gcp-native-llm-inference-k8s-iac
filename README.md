# LLM Cloud-Agnostic K8s Terraform

Cloud-agnostic, Terraform-driven deployment of Large Language Model (LLM) serving and interactive inference on Kubernetes (GKE, EKS, or AKS).

## Overview

This project provides a template and automation scripts for deploying an LLM (Large Language Model) inference server **and** an interactive Streamlit website to your choice of a managed Kubernetes cluster (GKE, EKS, or AKS) using Terraform. The stack is portable: you choose your cloud platform; the setup process remains the same.

## Features

- **Cloud-agnostic:** Deploy on Google Kubernetes Engine (GKE), Amazon Elastic Kubernetes Service (EKS), or Azure Kubernetes Service (AKS).
- **Terraform Infrastructure-as-Code:** All resources and configurations are defined in version-controlled Terraform files.
- **Kubernetes-native:** Model server and Streamlit UI run as containerized services with scalable deployment and secure networking.
- **Dynamic LLM Selection & Hot-Swap:**  
  The Streamlit interface features a dropdown menu that **automatically fetches and lists all public LLMs from HuggingFace** on load.  
    - At any time, you can pick any available model and click the **Use** button to:
      - Deploy the selected LLM,
      - Remove the previously deployed model,
      - Reset the chat session,
      - Instantly begin inference with your new model.
- **Reset Chat Button:**  
  A **Reset Chat** button is always present. Clicking it clears the current conversation history and resets the session for a fresh start—no need to reload the page. [[see implementation note](#feature-implementation-notes)]
- **User-Friendly Inference:**  
  All model inference happens directly from the deployed Streamlit web interface.
- **Easy Customization:** Adjust model, hardware requirements, and environment with minimal changes.
- **Open-Source Model Support:** Start with Llama-2 7B or swap in any open-access model.

## Quick Start

### Prerequisites

- GitHub account
- Terraform CLI and a compatible cloud CLI (`gcloud`, `aws`, or `az`)
- Access to GKE, EKS, or AKS (cloud account with sufficient permissions)
- `kubectl`
- [Optional] Docker, if building images locally

### Deployment Steps

1. **Clone the Repository**
   ```bash
   git clone https://github.com/sanskargupta551/llm-cloud-agnostic-k8s-terraform.git
   cd llm-cloud-agnostic-k8s-terraform
   ```

2. **Configure Terraform**
   - Edit `terraform/main.tf` and `terraform/variables.tf` to select your cloud provider and region.
   - Supply your cloud credentials as required (environment variables or configuration).

3. **Initialize and Apply**
   ```bash
   terraform init
   terraform plan
   terraform apply
   ```

4. **Access the Streamlit Inference UI**
   - After deployment, the output will display the external URL of your Streamlit web interface.
   - Open this link in your browser.

5. **Model Selection, Chat, and Inference**
   - At the top of the Streamlit interface, use the dropdown to **browse all public HuggingFace LLMs** (auto-fetched).
   - Select any model and click **Use**:
     - The new model will be provisioned and deployed.
     - The previous model (if any) will be automatically removed.
     - The chat/inference UI will reset for a fresh, context-free session with the new model.
   - Enter your prompt and run inference—the response will be shown in the UI.
   - Click **Reset Chat** at any time to clear the conversation history and start a new chat session with the current model.

   > **Tip:** You can switch models or reset the chat at any time. The system ensures only one LLM is active per session for efficient resource management.

## Directory Structure

```
llm-cloud-agnostic-k8s-terraform/
│
├── README.md                     # Project overview, instructions, badges
├── LICENSE                       # MIT License
├── .gitignore                    # Ignore system/build files and secrets
│
├── terraform/                    # All Terraform IaC code and environments
│   ├── main.tf
│   ├── variables.tf
│   ├── outputs.tf
│   ├── providers.tf
│   ├── versions.tf
│   ├── modules/
│   └── environments/
│
├── k8s/                          # Kubernetes deployment manifests
│   ├── deployment.yaml           # LLM serving Deployment spec
│   ├── service.yaml              # Service for model endpoint
│   ├── streamlit.yaml            # Streamlit UI Deployment spec
│   ├── streamlit-service.yaml    # Expose Streamlit app (LoadBalancer)
│   ├── ingress.yaml              # (Optional) Ingress or Gateway
│   ├── configmap.yaml            # (Optional) Config/Secrets for apps
│   └── hpa.yaml                  # (Optional) Horizontal pod autoscaling
│
├── streamlit_app/                # Streamlit webapp source code
│   ├── app.py                    # Main Streamlit Python script
│   ├── requirements.txt          # Python dependencies for Streamlit app
│   ├── utils.py                  # (Optional) Helper functions
│   ├── huggingface_helpers.py    # (Optional) HuggingFace API utils
│   └── assets/                   # (Optional) Images/static files
│
├── model/                        # (Optional) Model assets/configs
│   └── README.md
│
├── scripts/                      # Automation and helper scripts
│   ├── deploy.sh
│   ├── destroy.sh
│   └── validate.sh
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

- Llama-2 7B (default, for reference)
- **Any public text-generation LLM** from HuggingFace, selectable live in the Streamlit dropdown—no manual edits needed.

## License

This project is licensed under the **MIT License**.  
You are free to use, modify, and distribute with attribution.

## Contributing

Contributions, issues, and discussions are welcome! Please open an issue or submit a pull request for suggestions or improvements.

## Acknowledgements

- Meta AI (Llama-2)
- HuggingFace
- Streamlit
- Terraform, Kubernetes, and cloud providers GCP/AWS/Azure
- Open-source ML and infra communities

#### Feature Implementation Notes
- The **Reset Chat** button clears the conversation/session by resetting relevant variables in `st.session_state`.  
- Dynamic LLM fetching leverages the `huggingface_hub` Python library and displays only public, (license-)compliant text generation models.
- Model hot-swapping and deployment/removal are managed via Kubernetes calls from within the Streamlit backend, using appropriately scoped service accounts for security.

*Build your own portable, cloud-agnostic LLM inference stack—learn, customize, and deploy on your favorite cloud with just a few commands, browse any public LLM, and start inferring instantly through an interactive web UI!*