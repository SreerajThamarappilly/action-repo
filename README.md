# action-repo

This repository is responsible for sending GitHub events ("Push", "Pull Request", "Merge") to a registered webhook endpoint. The repository is configured to trigger webhooks when any of the defined GitHub actions occur, and those events are sent to a webhook server for processing and storage.

## Features

- **Trigger GitHub Webhooks**: This repository is configured to trigger a webhook on the following GitHub actions:
  - Push
  - Pull Request
  - Merge
- **Send Webhooks to a Registered Endpoint**: Webhooks are sent to the URL registered in the webhook settings of this repository.

## Webhook Configuration

The webhook is configured in GitHub repository settings to send payloads to the webhook server hosted in the [webhook-repo](https://github.com/SreerajThamarappilly/webhook-repo.git). The payload is sent whenever there are actions related to "Push", "Pull Request", or "Merge."

### 1. Setting Up the Webhook

1. Go to **Settings > Webhooks** in this repository.
2. Click **Add Webhook**.
3. In the **Payload URL** field, add the URL where the webhook-repo is hosted (e.g., `http://your-app-env.elasticbeanstalk.com/webhook`).
4. Set **Content Type** to `application/json`.
5. Select **"Send me everything"** under "Which events would you like to trigger this webhook?"
6. Click **Add Webhook**.

### 2. Branches

The webhook is configured to trigger for actions on all the branches of this repository.

- The repository monitors activities such as push, pull request, and merge on any branch.
  
In the GitHub Actions YAML file (`.github/workflows/main.yml`), the following branches are configured:

```yaml
on:
  push:
    branches:
      - '**'
  pull_request:
    branches:
      - '**'
```

### 3. Workflow Actions

The GitHub Actions workflow will trigger the webhook events when code is pushed or pull requests are made on any branch.

### 4. Sample Event Payload

- **Push Event:**: 

```json
{
  "request_id": "b72740da18b7c0d3d29b1ef28d3f51892615d37c",
  "author": "SreerajThamarappilly",
  "action": "PUSH",
  "from_branch": null,
  "to_branch": "develop",
  "timestamp": "2024-09-12T05:23:50Z"
}
```

- **Pull Request Event:**: 

```json
{
  "request_id": "b72740da18b7c0d3d29b1ef28d3f51892615d37d",
  "author": "SreerajThamarappilly",
  "action": "PULL_REQUEST_OPENED",
  "from_branch": "feature-branch",
  "to_branch": "develop",
  "timestamp": "2024-09-12T06:00:00Z"
}
```

- **Merge Event:**: 

```json
{
  "request_id": "b72740da18b7c0d3d29b1ef28d3f51892615d37d",
  "author": "SreerajThamarappilly",
  "action": "MERGE",
  "from_branch": "feature-branch",
  "to_branch": "develop",
  "timestamp": "2024-09-12T06:30:00Z"
}
```

## License

This project is licensed under the MIT License.
