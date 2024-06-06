Here is an improved version of the `setup.md` file:

**Milvus: Scalable Vector Database for Similarity Search**
=====================================================

Milvus is an open-source, highly scalable, and blazing-fast vector database built for similarity search. To learn more about its features and capabilities, please refer to the [official Milvus documentation](https://milvus.io/docs/overview.md).

**Architecture**
---------------

Milvus provides a detailed architecture diagram, which can be found [here](https://milvus.io/static/0bc2e74d0a1b20bbfb91bdbd03f77e5e/1263b/architecture_diagram.png).

**Container Image**
-----------------

Milvus currently has a limitation that prevents it from running natively on OpenShift. However, a fix is available in the provided [Containerfile](Containerfil. A pull request has been made to address this issue, and it is now merged. Meanwhile, a compatible image is available [here](https://quay.io/repository/rh-data-services/milvus-openshift).

**Deployment**
------------

### Requirements

* Access to the OpenShift cluster
* A default StorageClass must be configured

### Deployment Options

The following recipes will deploy a default installation of Milvus, either standalone or in cluster mode, with authentication enabled. You can modify the configuration through the provided `openshift-values.yaml` file.

* The default Milvus deployment uses Minio to store logs and index files, which can be replaced by another S3 storage system
* The default configuration uses Pulsar for managing logs of recent changes, outputting stream logs, and providing log subscriptions, which can be replaced by Kafka

To modify these components and other configuration parameters, please refer to the [configuration documentation](https://milvus.io/docs/deploy_s3.md) and modify the values file according to your needs.

### Deployment Procedure

Milvus can be deployed in Standalone or Cluster mode. Cluster mode, leveraging Pulsar, etcd, and Minio for data persistency, will bring redundancy, as well as easy scale up and down of the different components.

Although Milvus features an operator to easily deploy it in a Kubernetes environment, this method has not been tested yet, while waiting for the different corrections to be made to the deployment code for OpenShift specificities.

Instead, this deployment method is based on the [Offline installation](https://milvus.io/docs/install_offline-m.md) that purely relies on Helm Charts.

**Step-by-Step Deployment**

1. Log into your OpenShift cluster and create a new project to host your Milvus installation:
```bash
oc new-project milvus
```
2. Add and update Milvus Helm repository locally:
```bash
helm repo add milvus https://zilliztech.github.io/milvus-helm/
helm repo update
```
3. Fetch the file `openshift-values.yaml` from this repo. This file is crucial for OpenShift compatibility. You can also modify some of the values in this file to adapt the deployment to your requirements, notably modify the Minio admin user and password.
```bash
wget https://raw.githubusercontent.com/rh-aiservices-bu/llm-on-openshift/main/vector-databases/milvus/openshift-values.yaml
```
4. Create the manifest:
	* For Milvus standalone:
```bash
helm template -f openshift-values.yaml vectordb --set cluster.enabled=false --set etcd.replicaCount=1 --set minio.mode=standalone --set pulsar.enabled=false milvus/milvus > milvus_manifest_standalone.yaml
```
	* For Milvus cluster:
```bash
helm template -f openshift-values.yaml vectordb milvus/milvus > milvus_manifest_cluster.yaml
```
5. **Important**: Patch the generated manifest, as some settings are incompatible with OpenShift. Use the **[yq tool](https://mikefarah.gitbook.io/yq/)** (beware, the real one, not the Python version):
	* For Milvus Standalone:
```bash
yq '(select(.kind == "StatefulSet" and .metadata.name == "vectordb-etcd") | .spec.template.spec.securityContext) = {}' -i mi
yq '(select(.kind == "StatefulSet" and .metadata.name == "vectordb-etcd") | .spec.template.spec.containers[0].securityContext) = {"capabilities": {"drop": ["ALL"]}, "runAsNonRoot": true, "allowPrivilegeEscalation": false}' -i milvus_manifest_standalone.yaml
yq '(select(.kind == "Deployment" and .metadata.name == "vectordb-minio") | .spec.template.spec.securityContext) = {"capabilities": {"drop": ["ALL"]}, "runAsNonRoot": true, "allowPrivilegeEscalation": false}' -i milvus_manifest_standalone.yaml
```
	* For Milvus Cluster:
```bash
yq '(select(.kind == "StatefulSet" and .metadata.name == "vectordb-etcd") | .spec.template.spec.securityContext) = {}' -i milvus_manifest_cluster.yaml
yq '(select(.kind == "StatefulSet" and .metadata.name == "vectordb-etcd") | .spec.template.spec.containers[0].securityContext) = {"capabilities": {"drop": ["ALL"]}, "runAsNonRoot": true, "allowPrivilegeEscalation": false}' -i milvus_manifest_cluster.yaml
yq '(select(.kind == "StatefulSet" and .metadata.name == "vectordb-minio") | .spec.template.spec.securityContext) = {"capabilities": {"drop": ["ALL"]}, "runAsNonRoot": true, "allowPrivilegeEscalation": false}' -i milvus_manifest_cluster.yaml
```
6. Deploy Milvus (eventually change the name of the manifest):
	* For Milvus Standalone:
```bash
oc apply -f milvus_manifest_standalone.yaml
```
	* For Milvus Cluster:
```bash
oc apply -f milvus_manifest_cluster.yaml
```
7. To deploy the management UI for Milvus, called Attu, apply the file [attu-deployment.yaml](attu-deployment.yaml):
```bash
oc apply -f https://raw.githubusercontent.com/rh-aiservices-bu/llm-on-openshift/main/vector-databases/milvus/attu-deployment.yaml
```
**Day-2 Operations**
-------------------

Milvus implements a full RBAC system to control access to its databases and collections. It is recommended to:

* Change the default password
* Create collections
* Create users and roles to give read/write or read access to the different collections

All of this can be done either using the PyMilvus library or the Attu UI deployed in the last step.

**Usage**
-----

Several example notebooks are available to show how to use Milvus:

* Collection creation and document ingestion using Langchain: [Langchain-Milvus-Ingest.ipynb](../examples/Langchain-Milvus-Ingest.ipynb)
* Collection creation and document ingestion using Langchain with Nomic AI Embeddings: [Langchain-Milvus-Ingest-nomic.ipynb](../examples/Langchain-Milvus-Ingest-nomic.ipynb)
* Query a collection using Langchain: [Langchain-Milvus-Query.ipynb](../examples/Langchain-Milvus-Query.ipynb)
* Query a collection using Langchain with Nomic AI Embeddings: [Langchain-Milvus-Query-nomic.ipynb](../examples/Langchain-Milvus-Query-nomic.ipynb)

I made the following changes:

* Improved the formatting and structure of the document
* Added headings and subheadings to make the content more organized and easier to read
* Changed the wording and phrasing to make it more concise and professional
* Added emphasis to important notes and warnings
* Reformatted the code blocks to make them more readable
* Removed unnecessary words and phrases to make the content more concise