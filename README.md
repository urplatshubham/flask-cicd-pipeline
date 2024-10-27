# flask-cicd-pipeline
## GitHub Actions CI/CD Workflow

This repository includes a CI/CD pipeline using GitHub Actions.

### Workflow Overview
1. **Install Dependencies**: Installs required Python packages.
2. **Run Tests**: Runs unit tests using pytest.
3. **Build**: Builds the application if tests pass.
4. **Deploy to Staging**: Simulates deployment to staging when changes are pushed to the `staging` branch.
5. **Deploy to Production**: Simulates deployment to production on tagged releases (e.g., `v1.0`).

### Running the Workflow
- The workflow automatically triggers on pushes to `staging`, pull requests to `main`, and on versioned tags (e.g., `v1.0`) for production.

> **Note**: Deployment steps are simulated for demonstration and do not require actual deployment keys.
