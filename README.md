# cicd-build-push-on-gcp-action
This GitHub Action is designed to build and push an artifact to Google Container Registry (GCR). It simplifies the CI/CD process for deploying containerized applications on Google Cloud Platform (GCP).


## Inputs

### `release-version` (required)
The release version of the artifact to be built and pushed. This is used to tag the Docker image appropriately.

Example:
```yaml
release-version: '1.0.0'
```

### `gcr-auth-json` (required)
The JSON credential key for authenticating with Google Cloud. This is required for logging into GCP and pushing the image to GCR.

Example:
```yaml
gcr-auth-json: '${{ secrets.GCR_AUTH_JSON }}'
```

### `gcr-domain` (required)
The domain of the Google Container Registry (e.g., `europe-west4-docker.pkg.dev`).

Example:
```yaml
gcr-domain: 'europe-west4-docker.pkg.dev'
```

### `gcr-path` (required)
The GCR path where the artifact will be stored. This usually includes your GCP project ID and image name.

Example:
```yaml
gcr-path: 'my-gcp-project/my-repo'
```

## Outputs

### `image-gcp-url`
The full URL of the Docker image pushed to GCR.

Example output:
```
https://europe-west4-docker.pkg.dev/my-gcp-project/my-repo/devredops/cicd-build-push-on-gcp-action
```

## Usage

Below is an example of how to use this action in a GitHub workflow:
```yaml
name: Build and Push to GCP

on:
  push:
    branches:
      - main

jobs:
  build-and-push:
    runs-on: ubuntu-latest

    steps:
    - name: Checkout code
      uses: actions/checkout@v2

    - name: Build and Push Docker Image to GCP
      uses: devredops/cicd-build-push-on-gcp-action@v1
      with:
        release-version: '1.0.0'
        gcr-auth-json: ${{ secrets.GCR_AUTH_JSON }}
        gcr-domain: 'europe-west4-docker.pkg.dev'
        gcr-path: 'my-gcp-project/my-repo'
```

---

## Setting Up This Action
This project includes several useful resources to help you get started:
  - [Ruby on Rails Project](https://github.com/devredops/cicd-release-action/blob/main/docs/ruby-on-rails.md)

---
