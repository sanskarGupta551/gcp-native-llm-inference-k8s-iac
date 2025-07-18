# llm-cloud-agnostic-k8s-terraform

**Cloud-agnostic, self-cleaning LLM serving with Kubernetes & Terraform — deploy, chat, and manage public Hugging Face models on AWS, GCP, or Azure.**

## 🌟 Project Overview

**llm-cloud-agnostic-k8s-terraform** lets you launch, interact with, and safely destroy a large language model (LLM) cloud infrastructure—end-to-end—on your favorite cloud platform (Google Cloud, AWS, or Azure) using Kubernetes, GPUs, and modern MLOps best practices.  
Run a local Streamlit app to select, deploy, and chat with public Hugging Face LLMs in a live, production-like setup.

## 🚀 Features

- **Cloud Agnostic:** Provision GKE, EKS, or AKS clusters via Terraform for GCP, AWS, or Azure.
- **Production-grade Serving:** GPU-enabled LLM inference with high security, dynamic scaling, and observability.
- **Modern User Experience:** Local Streamlit chat interface with dynamic Hugging Face model listing, one-click deployment, and context-aware conversations.
- **Self-cleaning Infrastructure:**  
  - **Auto Idle Cleanup** – resources are auto-destroyed after inactivity  
  - **Manual “Clean-up Resources” Button** in the UI  
  - **Cleanup scripts** for every provider  
- **Security First:** Cloud-native secrets, private networking, role-based access.
- **Easy Teardown, Clear Documentation, No Hidden Costs!**

## 🏗️ Architecture

- **Kubernetes Cluster (GKE/EKS/AKS):** GPU-enabled LLM inference backend (vLLM, TGI).
- **Cloud-native services:** Artifact/Container registry, secret manager, monitoring/logging, load balancer.
- **Streamlit Web App (Local):** Dropdown Hugging Face model selector, deploy/reset chat buttons, chat interface, real-time context.
- **Multi-layered cleanup:** Idle auto-destroy, manual in-app button, and scripts.

## ⚡ Quickstart

```bash
# 1. Choose your cloud provider and prepare credentials (see the relevant folder's README)
cd deployments/gcp   # or aws or azure

# 2. Deploy (edit variables as needed)
terraform init
terraform apply

# 3. The local Streamlit UI launches automatically!

# 4. Select, deploy, and chat with an LLM via the web app

# 5. CLEAN-UP: Use the “Clean-up Resources” button in the app,
#    wait for auto-cleanup, or run ./cleanup.sh when done.
```

## 🧹 Resource Cleanup

We offer three ways to keep your cloud bill at zero:
- **Automatic cleanup** — the infrastructure is destroyed after a period of inactivity
- **In-app cleanup button** — click to delete everything
- **Manual script** — each cloud folder includes a single-command cleanup script

## 👩‍💻 For Potential Employers

- Demonstrates real-world, cloud-native MLOps skills (multi-cloud, IaC, production LLM ops, resource controls)
- Modular, readable Terraform and app code
- Complete and self-contained: setup, deploy, chat, teardown, all in minutes

## 📚 Documentation

- Each `/deployments/{provider}/` folder includes detailed instructions.
- See [docs/architecture.md](docs/architecture.md) for deep dives on features, security, and best practices.

## 📝 License

MIT — see `LICENSE`

**Build, serve, chat, and walk away—your cloud is always clean with llm-cloud-agnostic-k8s-terraform!**