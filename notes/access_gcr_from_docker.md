
## Accessing Google Container Registry from Docker

Create a service account with a key in JSON format or add a new key
```text
Google Cloud Platform -> IAM -> Service Accounts
```

Store the key in `~/secret.json` file and login to GCR using Docker
```console
docker login -u _json_key -p "$(cat ~/secret.json)" eu.gcr.io
```

An entry for `eu.gcr.io` will be created in `~/.docker/config.json`

