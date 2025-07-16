# gcp-native-llm-inference-k8s-iac

GCP-native Infrastructure-as-Code (IaC) automation for deploying and managing Large Language Model (LLM) inference and an interactive Streamlit UI on Kubernetes (K8s) clusters, using fully native Google Cloud services—scalable, one-click, and no-code via Cloud Shell.

## Overview

This repository provides everything required to deploy and manage LLM inference on Google Kubernetes Engine (GKE), orchestrated by Terraform (Google Cloud-native IaC), with a dynamic, user-friendly Streamlit web interface. Entirely GCP-native, it enables seamless provisioning, secure resource management, and automated serving of open-source LLMs sourced from HuggingFace, all through your browser.

## Features

- **GCP-Native Only:** No cross-cloud dependencies; all infrastructure, authentication, and pipeline automation use Google Cloud best practices.
- **One-Click, No-Code Deployment:**  
  Instant onboarding using the "Open in Cloud Shell" button for completely hands-off end-to-end setup.
- **Google Kubernetes Engine (GKE):**  
  LLM model servers and the Streamlit UI run as scalable pods/services with Google-native security and networking.
- **Terraform (GCP modules):**  
  All infrastructure—GKE clusters, IAM, networking, container registry, and backend resources—provisioned with Google’s own Terraform provider and modules.
- **Dynamic LLM Selection & Hot-Swap:**  
  The Streamlit UI auto-fetches all public, compliant HuggingFace LLMs.  
  Users can:
  - Pick and deploy any available model,
  - Tear down previous models automatically,
  - Reset chat instantly with each switch.
- **Reset Chat Functionality:**  
  "Reset Chat" button always accessible to clear the session for a fresh interaction.
- **IAM, Networking, and Cost Controls:**  
  Utilizes GCP-native identity, security, private networking, and cost management practices.
- **Extensible:**  
  Easily customize hardware profiles, GKE nodepools, API scopes, and add Vertex AI or other GCP services as needed.

## Quick Start

### Prerequisites

- Google (GCP) account with billing enabled and project/organization permissions
- IAM roles: Owner/Editor or roles for GKE Admin, Compute Admin, Service Account Admin, and Artifact Registry access
- [Optional] Basic familiarity with GKE, GCP Console

### One-Click Deployment

#### 1. Open in Google Cloud Shell

## One-Click Deployment

[![Open in Cloud Shell](https://gstatic.com/cloudssh/images/open-btn.svg)](https://console.cloud.google.com/cloudshell/open?git_repo=https://github.com/yourusername/gcp-native-llm-inference-k8s-iac&open_in_editor=true&working_dir=gcp-native-llm-inference-k8s-iac)



#### 2. Follow the On-Screen Prompts

- **Auth and Project Selection:**  
  If prompted, log in to your Google account and choose the target project.
- **Run the Deployment Script:**  
  Cloud Shell may auto-prompt; otherwise, run:
  ```sh
  ./scripts/deploy.sh
  ```
- The script will:
  - Enable required GCP APIs (Kubernetes Engine, Compute, Artifact Registry, IAM, etc.)
  - Provision the GKE cluster and networking
  - Build/push required container images (if needed)
  - Apply Kubernetes manifests for the LLM server and Streamlit app
  - Output the public URL of your Streamlit web interface

#### 3. Access the Streamlit Web Interface

- Click the provided URL in your Cloud Shell output to launch the inference UI.

#### 4. Use the Application

- **Model Selection:**  
  At the top of the Streamlit app, use the dropdown to browse auto-fetched public HuggingFace LLMs.
- **Deploy:**  
  Select any model, click **Use** to deploy (the previous deployment is replaced, and chat resets automatically).
- **Inference:**  
  Enter a prompt and view the model’s response.  
  Click **Reset Chat** at any time to start fresh with the current model.

## Directory Structure

```
gcp-native-llm-inference-k8s-iac/
│
├── README.md                           # Project overview and usage
├── LICENSE                             # MIT License
├── .gitignore
│
├── terraform/                          # GCP-native IaC configuration
│   ├── main.tf
│   ├── variables.tf
│   ├── outputs.tf
│   ├── providers.tf
│   ├── versions.tf
│   ├── modules/                        # (Optional) Custom/shared modules
│
├── k8s/                                # GKE deployment manifests
│   ├── deployment.yaml                 # LLM server deployment spec
│   ├── service.yaml                    # Model endpoint service
│   ├── streamlit.yaml                  # Streamlit app deployment
│   ├── streamlit-service.yaml
│   ├── configmap.yaml
│   └── hpa.yaml                        # (Optional) Autoscaling
│
├── streamlit_app/                      # Streamlit webapp source
│   ├── app.py
│   ├── requirements.txt
│   ├── huggingface_helpers.py
│   └── assets/                         # (Optional) UI static files
│
├── scripts/
│   ├── deploy.sh                       # End-to-end infra & app setup
│   ├── destroy.sh                      # Full teardown script
│
├── docs/
├── assets/
```

## Supported Models

- **Llama-2 7B (default, reference)**
- **Any public, compliant text-generation LLM** from HuggingFace—listed live in the UI dropdown, deployable with one click.

## License

This project is licensed under the **MIT License**.  
Free to use, modify, and distribute with attribution.

## Contributing

Issues, suggestions, and pull requests are welcome!

## Acknowledgements

- Meta AI (Llama-2)
- HuggingFace
- Streamlit
- Google Cloud Platform—GKE, Artifact Registry, IAM, and Terraform modules
- GCP MLOps and open-source AI communities

*Build your own portable, fully GCP-native LLM inference stack—learn, customize, and deploy on Google Cloud with a single click, browse any public HuggingFace LLM, and start inferring instantly through a dynamic, interactive web UI!*
