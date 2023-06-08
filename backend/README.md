
## Backend Getting Started

It contains these folders and files, following our recommended project layout:

File or Folder | Purpose
---------|----------
`db/` | your domain models and data go here
`docker/` | Dockerfile
`k8s/` | kubernetes deployment files
`srv/` | your service models and code go here
`package.json` | project metadata and configuration
`README.md` | this getting started guide


## Next Steps

- Open a new terminal and run `cds watch` 
- (in VS Code simply choose _**Terminal** > Run Task > cds watch_)
- Start adding content, for example, a [db/schema.cds](db/schema.cds).
- Learn more at https://cap.cloud.sap/docs/get-started/.


## Steps

### Run the backend locally

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

The application loads at `http://localhost:4004`. admin service endpoints use `alice` as default username, not need password.

### Build the Docker image

1. Build

   ```shell
   docker build -t <your-docker-id>/sap-cap-on-kyma-kt-202306:backend-v1.0.0 -f docker/Dockerfile .
   ```

2. To run the image locally, adjust the value of the **API_URL** parameter in the `webapp/config.js` file and mount it into the image:

   ```shell
   docker run -p 4004:4004 <your-docker-id>/sap-cap-on-kyma-kt-202306:backend-v1.0.0 --name sap-cap-on-kyma-kt-202306-backend
   ```

3. Push the image to your Docker repository:

   ```shell
   docker login
   docker push <your-docker-id>/sap-cap-on-kyma-kt-202306:backend-v1.0.0
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
