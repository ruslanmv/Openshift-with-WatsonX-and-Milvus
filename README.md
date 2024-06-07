
# Openshift with WatsonX and Milvus for Multimodal


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


-----

## Additional Examples:

| **Type**        | **Description** | **Link** |
|-----------------|-----------------|----------|
| **Openshift**   | Collection creation and document ingestion using Langchain | [Langchain-Milvus-Ingest.ipynb](./examples/Langchain-Milvus-Ingest.ipynb) |
|                 | Collection creation and document ingestion using Langchain with Nomic AI Embeddings | [Langchain-Milvus-Ingest-nomic.ipynb](./examples/Langchain-Milvus-Ingest-nomic.ipynb) |
|                 | Query a collection using Langchain | [Langchain-Milvus-Query.ipynb](./examples/Langchain-Milvus-Query.ipynb) |
|                 | Query a collection using Langchain with Nomic AI Embeddings | [Langchain-Milvus-Query-nomic.ipynb](./examples/Langchain-Milvus-Query-nomic.ipynb) |
| **Introduction**| An introduction to `Pipeline`, which can help you better learn the data processing pipeline with Towhee. | [Getting Started with Pipeline](./examples/pipeline) |
| **Image**       | Search for images that are similar or related to the input image, it supports a lot of models such as ResNet, VGG, EfficientNet, ViT, etc. | [Reverse Image Search](./examples/image/reverse_image_search) |
|                 | Convert an image into an animated image. | [Image Animation](./examples/image/image_animation) |
|                 | Find exact or near-exact duplicates within a collection of images. | [Image Deduplication](./examples/image/image_deduplication) |
|                 | Returns images related to the description of the input query text, which is cross-modal retrieval. | [Text Image Search](./examples/image/text_image_search) |
|                 | Under the hood: Embedding models and ANNS indexes in image search. | [Visualization](./examples/image/visualization) |
| **NLP**         | Process user questions and give answers through natural language technology. | [Q&A System](./examples/nlp/question_answering) |
|                 | Search most similar text to the query text across all data. | [Text Search](./examples/nlp/text_search) |
| **Video**       | It takes a video as input to search for similar videos. | [Reverse Video Search](./examples/video/reverse_video_search) |
|                 | Video Classification is the task of producing a label that is relevant to the video given its frames. | [Video Classification](video/video_tagging) |
|                 | Search for similar or related videos with the input text. | [Text Video Search](./examples/video/text_video_retrieval) |
|                 | Predict the probability of a fake video for a given video. | [Deepfake Detection](./examples/video/deepfake_detection) |
| **Audio**       | Categorize certain sounds into certain categories, such as ambient sound classification and speech recognition. | [Audio Classification](./examples/audio/audio_classification) |
| **Medical**     | Search for similar molecular formulas based on the Tanimoto metric, and also supports searching for substructures and superstructures. | [Molecular Search](./examples/medical/molecular_search) |
| **Data Science**| Predict whether the bank issues a credit card to the applicant, and the credit scores can objectively quantify the magnitude of risk. | [Credit Card Approval Prediction](./examples/data_science/credit_card_approval_prediction) |
| **Training**    | Tutorial about how to fine tune with Towhee. | [Fine Tune](./examples/fine_tune) |

Note
----
We welcome new contributions! If you have any interesting examples or improvements, feel free to submit a pull request.
In repository we have many interesting examples that use Towhee to process various unstructured data like images, audio, video, etc. 
These demo is for educational purposes only and is not intended for production use. Please ensure you have the necessary permissions and licenses to use the required components.

License
-------

This repository is licensed under the Apache 2.0 License. See the LICENSE file for details.