
# Openshift with WatsonX and Milvus for Multimodal
==============================================

This repository demonstrates the implementation of Multimodal with WatsonX and Milvus on OpenShift. It showcases the integration of LangChain, WatsonX, and Milvus to build a knowledge graph with multimodal capabilities.

What is Multimodal RAG with Milvus?
--------------------------------

Multimodal RAG (Retrieval-Augmented Generation) with Milvus enables the combination of images and text queries to retrieve relevant information from a knowledge graph.

Advantages of using Multimodal on OpenShift with Milvus and WatsonX
----------------------------------------------------------------

* Scalable and highly performant multimodal search capabilities
* Integration with WatsonX for AI-powered knowledge graph construction
* Leverages Milvus' vector database for efficient similarity search

Components
----------

* OpenShift: Cluster Environment
* LangChain: A Python library for building and integrating AI models
* WatsonX: A cloud-based AI platform for building and deploying AI models
* Milvus: A relational database management system with vector database

Demo Overview
------------

This demo showcases the following components:

* Document and Images loading and data preparation using LangChain
* Building a knowledge graph using LangChain and WatsonX
* Creating a vector store with Milvus
* Implementing RAG Multimodal using LangChain and WatsonX
* Querying the knowledge graph using natural language to retrieve images and text

Setup
-----

To run this demo, you'll need to:

1. Create an OpenShift instance with Elyra
2. Create a Milvus server [here](milvus/README.md)
3. Create a Watson Machine Learning (WML) Service instance
4. Install the required dependencies, including LangChain, WatsonX, and PgVector
5. Set up a Milvus instance
6. Load the demo data into the database

Running the Demo
---------------

To run the demo, simply execute the provided Python script. The script will guide you through the Multimodal demo, from document loading to querying the knowledge graph.

Examples of Milvus
-----

In repository we have many interesting examples that use Towhee to process various unstructured data like images, audio, video, etc. You can easily run these examples on your machine.
[here](./examples/README.md)

Note
----

This demo is for educational purposes only and is not intended for production use. Please ensure you have the necessary permissions and licenses to use the required components.

License
-------

This repository is licensed under the Apache 2.0 License. See the LICENSE file for details.