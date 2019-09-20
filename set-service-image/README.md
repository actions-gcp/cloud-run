# Update Cloud Run service image

This [GitHub Action][action] changes the Docker image associated with
a [Cloud Run][run] service. It can be used to deploy a new image built
and pushed in earlier steps of a workflow.

`cloud-run/set-service-image` requires a [service account][sa] with
[permissions][perms] to update the service and to act as the Cloud Run
runtime service account. A JSON key for that service account should
be stored as a GitHub secret and supplied as the `key` input.

## Inputs

| Name          | Description                     |
| ------------- | ------------------------------- |
| *project*     | Google Cloud project ID         |
| *location*    | Cloud Run location              |
| *service*     | Cloud Run service name          |
| *image*       | Docker image name               |
| *key*         | JSON [service account key][key] |

## Usage

```yaml
      - uses: actions-gcp/cloud-run/set-service-image@master
        with:
          project:  <project-id>
          location: us-central1
          service:  test
          image:    gcr.io/<project-id>/test:${{ github.sha }}
          key:      ${{ secrets.SERVICE_ACCOUNT_KEY }}

```

[action]: https://github.com/features/actions
[run]:    https://cloud.google.com/run/
[sa]:     https://cloud.google.com/compute/docs/access/service-accounts
[perms]:  https://cloud.google.com/run/docs/reference/iam/roles#additional-configuration
[key]:    https://console.cloud.google.com/apis/credentials/serviceaccountkey
