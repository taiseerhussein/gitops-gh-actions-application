# GitOps & GitHub Actions CI/CD Example

This repository works in concert with [this manifest repository](https://github.com/evanshortiss/gitops-gh-actions-manifests)
to create a continuous delivery pipeline with OpenShift GitOps (based on Argo CD).

Code changes in this repository will trigger a workflow that builds this
application into a container image. Once the build is complete, it will trigger
a [workflow](https://github.com/evanshortiss/gitops-gh-actions-manifests/blob/main/.github/workflows/update-container-image.yaml)
that creates a PR in the manifest repository that updates it to use the new
container image. Merging this PR will automatically deploy the new container
image on your OpenShift or Kubernetes cluster.

## Configure the Build

Enabling the end-to-end CI/CD process requires setting the following variables in
the */settings/secrets/actions* page of this repository.

* QUAY_USERNAME
* QUAY_PASSWORD
* PAT

These variables are used in the [CI workflow](https://github.com/evanshortiss/gitops-gh-actions-application/blob/main/.github/workflows/build-container-image.yaml).

The `QUAY_USERNAME` and `QUAY_PASSWORD` variables are credentials for a quay.io
Robot Account that will be used to push the container image to the quay.io 
container registry. You can create a Robot Account and set permissions for Robot
Accounts in your Account Settings on quay.io. You can use Docker Hub or another
registry if you prefer, just remember to update the target **registry** CI
workflow.

The `PAT` is a fine-grained GitHub personal access token. Create a PAT from
your [Developer Settings](https://github.com/settings/tokens?type=beta) page.
While creating the PAT, you should:

1. Set **Repository access** to your fork of the [manifest repository](https://github.com/evanshortiss/gitops-gh-actions-manifests).
1. Configure **Permissions** to enable **Read and Write** access to **Actions**.

## Local Development

```bash
npm ci
npm run dev
```

Open [http://localhost:3000](http://localhost:3000) to view the application in a browser.
