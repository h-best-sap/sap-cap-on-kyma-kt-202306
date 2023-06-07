## Overview

This sample provides a Node.js CAP Service application service to demonstrate how to:

- Create a development Namespace in the Kyma runtime.
- Configure and build an CAP Service Docker image.
- Deploy the CAP Service in the Kyma runtime which includes:
  - A Deployment of the CAP Service.
  - An API to expose the service externally.

## Prerequisites

- [Node.js](https://nodejs.org/en/)
- [ui5 cli](https://sap.github.io/ui5-tooling/pages/CLI/)
- [cds sdk](https://cap.cloud.sap/docs/get-started/jumpstart#_2-install-cap-s-cds-dk)
- [SAP BTP, Kyma runtime instance](https://cockpit.hanatrial.ondemand.com/trial/#/home/trial)
- [Docker](https://www.docker.com/)
- [Docker Hub](https://hub.docker.com)
- [kubectl](https://kubernetes.io/docs/tasks/tools/install-kubectl/) configured to use the `KUBECONFIG` file downloaded from the Kyma runtime.
- [kubelogin](https://github.com/int128/kubelogin/releases), remane it to `kubectl-oidc_login.exe`

Optionals:

- VS Code plugins: SAP CDS Language Support， SAP Fiori tools - Extension Pack
- [SQLite](https://sqlite.org/download.html), [VS Code sqltools](https://marketplace.visualstudio.com/items?itemName=mtxr.sqltools)

## Getting Started

It contains these folders and files, following our recommended project layout:

File or Folder | Purpose
---------|----------
`app/` | content for UI frontends goes here
`db/` | your domain models and data go here
`docker/` | Dockerfile
`k8s/` | kubernetes deployment files
`srv/` | your service models and code go here
`package.json` | project metadata and configuration
`readme.md` | this getting started guide


## Next Steps

- Open a new terminal and run `cds watch` 
- (in VS Code simply choose _**Terminal** > Run Task > cds watch_)
- Start adding content, for example, a [db/schema.cds](db/schema.cds).
- Learn more at https://cap.cloud.sap/docs/get-started/.


## Steps

### Run the frontend locally

1. Clone the project.
   ```shell
   git clone https://github.com/h-best-sap/sap-cap-on-kyma-kt-202306.git
   ```

2. Inside the directory, run:

   ```shell
   cd sap-cap-on-kyma-kt-202306
   npm i
   ```

3. Verify the CAP tools install by running

   ```shell
   ## npm i -g @sap/cds-dk
   cds
   ```

4. Deploy the DB schemas to you local `sqlite` database

   ```shell
   cds deploy --to sqlite
   ```

5. Run the app using the command

   ```shell
   cds watch
   ```

The application loads at `http://localhost:4004`.

### Build the Docker image

1. Build and push the image to your Docker repository:

   ```shell
   docker build -t <your-docker-id>/sap-cap-on-kyma-kt-202306 -f docker/Dockerfile .
   docker push {your-docker-account}/sap-cap-on-kyma-kt-202306
   ```

2. To run the image locally, adjust the value of the **API_URL** parameter in the `webapp/config.js` file and mount it into the image:

   ```shell
   docker run -p 4004:4004 <dockerid>/sap-cap-on-kyma-kt-202306:latest --name sap-cap-on-kyma-kt-202306
   ```

### Deploy the application

1. Create a new `dev` Namespace:

   ```shell
   kubectl create namespace dev
   kubectl label namespaces dev istio-injection=enabled
   ```

2. Apply the Resources:

   ```shell
   kubectl -n dev apply -f ./k8s/deployment.yaml
   kubectl -n dev apply -f ./k8s/apirule.yaml
   ```

3. Use the APIRule to open the application:

   ```shell
   https://sap-cap-on-kyma-kt-202306.{cluster-domain}
   ```

### Refers

- Examples with HANA DB
   - <https://www.youtube.com/watch?v=kwKr4JbscvY>
   - <https://sap-samples.github.io/cloud-cap-risk-management/Kyma/#add-sap-hana-cloud>
- cap get started
   - https://pages.github.tools.sap/cap/docs/get-started/in-a-nutshell
