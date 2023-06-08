## Overview

This sample provides `a Node.js CAP backend service` and `a frontend fiori application` service to demonstrate how to:

- Create a development Namespace in the Kyma runtime.
- Configure and build an CAP Service and fiori application Docker image.
- Deploy the them in the Kyma runtime which includes:
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
