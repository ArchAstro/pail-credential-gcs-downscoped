# pail-credential-gcs-downscoped

A [pail](https://pail.build) credential provider: your gcloud login, downscoped to the one repository (GCS Credential Access Boundary).

```sh
pail auth install gcs-downscoped
pail auth use gcs-downscoped --for gs://your-bucket --global
```

A pail credential provider (pail-credential/1) that hands pail a Google token downscoped to one
repository: read and write objects under gs://<bucket>/<prefix>/ and nothing else.

It is the reference for what a broker does server-side (exchange a broad credential for a
narrow, short-lived one with a Credential Access Boundary). Here the broad credential is
the caller's own gcloud login; a broker would use its service account instead and decide
first whether the caller may have the repository at all.

  pail auth install gcs-downscoped && pail auth use gcs-downscoped --for gs://acme-vcs

Optional: SOURCE_TOKEN_CMD (default `gcloud auth print-access-token`).

It speaks `pail-credential/1`: `pail-credential-gcs-downscoped get` reads `{"protocol","store","scheme"}` on stdin and prints
`{"token","expires_at"}`. `pail-extension.json` tells `pail auth install` which file to install.
