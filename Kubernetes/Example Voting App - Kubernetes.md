# Example Voting App - Kubernetes Manifests

This repository contains the Kubernetes specification files for the multi-container Example Voting App, sourced from the official KodeKloud repository.

---

## Repository Overview
* **Source Repository:** [KodeKloudHub Example Voting App](https://github.com/kodekloudhub/example-voting-app)
* **Manifest Directory:** [k8s-specifications Folder](https://github.com/kodekloudhub/example-voting-app/tree/master/k8s-specifications)

---

## Architecture & Components
The `k8s-specifications` directory includes deployment and service manifests for the following application tiers:
* **Vote App:** Front-end web app letting users vote between options.
* **Redis:** In-memory data store capturing incoming votes.
* **Worker:** .NET/Java background worker processing votes from Redis and storing them in PostgreSQL.
* **PostgreSQL:** Database persisting vote results.
* **Result App:** Front-end web app displaying the live results of the voting.

---

## Quick Deployment Steps

1. **Clone or fork the repository:**
   ```bash
   git clone [https://github.com/kodekloudhub/example-voting-app.git](https://github.com/kodekloudhub/example-voting-app.git)
   cd example-voting-app/k8s-specifications