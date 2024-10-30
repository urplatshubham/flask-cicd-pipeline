# Flask CI/CD Pipeline with GitHub Actions
This repo showcases a simple Flask app and a GitHub Actions workflow that handles basic CI/CD tasks – from installing dependencies to simulating staging and production deployments.

## Overview

This project includes a minimal Flask app with a single route and a GitHub Actions pipeline to automate testing, building, and "deploying" the app (just for show, no actual servers involved).

The workflow covers:
1. **Installing dependencies** – sets up the app with everything it needs to run.
2. **Running tests** – executes basic tests to ensure the app works.
3. **Building the app** – just a placeholder step to show build progress.
4. **Deploying to Staging** – runs if we push code to the `staging` branch.
5. **Deploying to Production** – runs on tagged releases (like `v1.0`) for production.

### Getting Started

If you want to try this out, clone the repo and check out the basic Flask setup in `app.py`. The app’s pretty straightforward; it just returns “Hello, GitHub Actions CI/CD!” on the homepage. There’s also a test in `test_app.py` to keep things honest.

#### Running the App Locally
Make sure you have Python 3.8+ installed. Then install the dependencies:

```bash
pip install -r requirements.txt
```

Run the app:

```bash
python app.py
```

### GitHub Actions Workflow

The real focus here is the GitHub Actions workflow. Here's a rundown of what it does:

- **Install Dependencies**: Sets up Python and installs the requirements.
- **Run Tests**: Runs `pytest` to check if the app is working as expected.
- **Build**: Just a placeholder build step.
- **Deploy to Staging**: Simulated deployment when pushing to `staging` branch.
- **Deploy to Production**: Simulated deployment on a version tag push, e.g., `v1.0`.

### Workflow Triggers
The CI/CD workflow triggers on:

- Pushes to the `staging` branch (to simulate staging deployment).
- Pull requests targeting the `main` branch.
- Versioned tags (like `v1.0`) to simulate production deployment.

### Running the Workflow

Push changes to the `staging` branch to simulate staging deployment, or tag a release (e.g., `v1.0`) to simulate production deployment. The steps will be logged in the **Actions** tab under your repo.

### Important Notes
> **Note**: This pipeline is only a simulation – no actual deployments to staging or production servers happen here, and no secrets are needed.

### Screenshots of Deployment done
![Screenshot (780)](https://github.com/user-attachments/assets/9e556579-2367-4b15-91b7-949f1080324f)
![Screenshot (779)](https://github.com/user-attachments/assets/e2b73aa6-6a61-4469-9b11-14618562d3e9)



