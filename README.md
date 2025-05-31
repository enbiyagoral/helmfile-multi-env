# Helmfile Multi-Environment Starter Kit

A multi-environment starter kit for Kubernetes deployment management using Helmfile. Provides separate configurations for development, staging, and production environments, offering customizable values and service configurations for each environment.

## Requirements

- Helm v3.x
- Helmfile
- kubectl
- Kubernetes cluster

## Installation

1. Install required tools:
   ```bash
   # Helm
   curl https://raw.githubusercontent.com/helm/helm/main/scripts/get-helm-3 | bash

   # Helmfile
   brew install helmfile
   ```

2. Clone the repository:
   ```bash
   git clone https://github.com/enbiyagoral/helmfile-multi-env.git
   cd helmfile-multi-env
   ```

3. Set environment variables:
   ```bash
   export KUBECONFIG=/path/to/your/kubeconfig
   ```

## Project Structure

```
.
├── charts/                    # Helm charts
│   └── nginx/                # Example Nginx chart
│       ├── Chart.yaml        # Chart metadata
│       ├── templates/        # Kubernetes manifest templates
│       └── values.yaml       # Default values
│
└── helmfile.d/               # Helmfile configurations
    ├── env/                  # Environment-based configurations
    │   ├── dev.yaml         # Development environment
    │   ├── stg.yaml         # Staging environment
    │   └── prod.yaml        # Production environment
    │
    └── values/              # Environment-based values
        ├── dev/             # Development values
        ├── stg/             # Staging values
        └── prod/            # Production values
```

## Components

### Charts
- `charts/`: Directory containing Helm charts
- Can create a separate chart for each service

### Helmfile Configurations
- `helmfile.d/`: Main configuration directory
- `env/`: Environment-based configurations
  - Separate YAML file for each environment
  - Environment-specific chart versions and values
- `values/`: Environment-based values
  - Separate value files for each environment
  - Service-based customizations

## Usage

1. There are two ways to add a new service:
   - Method 1: Create your own chart
     - Create a new chart under `charts/`
     - Add value files under `helmfile.d/values/{RELEASE_NAME}/`
     - Add the service to environment files under `helmfile.d/env/`
   
   - Method 2: Use an existing chart
     - Create value files under `helmfile.d/values/{RELEASE_NAME}/`
     - Add the service to environment files under `helmfile.d/env/`
     - Specify chart repository and version

2. To deploy:
   ```bash
   # For development environment
   helmfile -f helmfile.d/env/dev.yaml apply

   # For staging environment
   helmfile -f helmfile.d/env/stg.yaml apply

   # For production environment
   helmfile -f helmfile.d/env/prod.yaml apply
   ```

## Best Practices

### Value Management
- Use separate value files for each release (`values/{RELEASE_NAME}/values.yaml`)
- Manage secrets as separate files (`values/{RELEASE_NAME}/secrets.yaml`)

If you find this project helpful, please give it a ⭐️!
