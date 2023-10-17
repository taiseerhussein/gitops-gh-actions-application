# GitOps & GitHub Actions CI/CD Example

This repository works in concert with [this manifest repository](https://github.com/evanshortiss/gitops-gh-actions-manifests)
to create a continuous delivery pipeline with OpenShift GitOps (based on Argo CD).

Code changes in this repository will trigger a workflow that builds this
application into container image. Once the build is complete, it will trigger
a workflow in the [manifest repository](https://github.com/evanshortiss/gitops-gh-actions-manifests)
that creates a PR in the manifest repository that points to the new container
image. Merging this PR will automatically deploy the new container image on
your OpenShift or Kubernetes cluster.

## Configure the Build

Enabling the end-to-end CI process requires setting the following variables in
the */settings/secrets/actions* page of the repository.

* QUAY_USERNAME
* QUAY_PASSWORD
* PAT

## Local Development

```bash
npm ci
npm run dev
```

Open [http://localhost:3000](http://localhost:3000) to view the application in a browser.
