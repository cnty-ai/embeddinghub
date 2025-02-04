<h1 align="center">
	<img width="300" src="https://raw.githubusercontent.com/featureform/embeddings/main/assets/featureform_logo.png" alt="featureform">
	<br>
</h1>

<div align="center">
	<a href="https://github.com/featureform/embeddings/actions"><img src="https://img.shields.io/badge/featureform-workflow-blue?style=for-the-badge&logo=appveyor" alt="Embedding Store workflow"></a>
    <a href="https://pypi.org/project/embeddinghub/" target="_blank"><img src="https://img.shields.io/pypi/dm/embeddinghub?style=for-the-badge&logo=appveyor" alt="PyPi Downloads"></a>
    <a href="https://join.slack.com/t/featureform-community/shared_invite/zt-xhqp2m4i-JOCaN1vRN2NDXSVif10aQg" target="_blank"><img src="https://img.shields.io/badge/Join-Slack-blue?style=for-the-badge&logo=appveyor" alt="Featureform Slack"></a>
    <br>
    <a href="https://www.python.org/downloads/" target="_blank"><img src="https://img.shields.io/badge/python-3.6%20|%203.7|%203.8-brightgreen.svg" alt="Python supported"></a>
    <a href="https://pypi.org/project/embeddinghub/" target="_blank"><img src="https://badge.fury.io/py/embeddinghub.svg" alt="PyPi Version"></a>
    <a href="https://www.featureform.com/"><img src="https://img.shields.io/website?url=https%3A%2F%2Fwww.featureform.com%2F?style=for-the-badge&logo=appveyor" alt="featureform Website"></a>  
    <a href="https://twitter.com/featureformML" target="_blank"><img src="https://img.shields.io/twitter/url/http/shields.io.svg?style=social" alt="Twitter"></a>


	
</div>

<div align="center">
    <h3 align="center">
        <a href="https://www.featureform.com/">Website</a>
        <span> | </span>
        <a href="https://docs.featureform.com/">Docs</a>
        <span> | </span>
        <!-- <a href="https://apidocs.featureform.com/">API Docs</a>
        <span> | </span> -->
        <a href="https://join.slack.com/t/featureform-community/shared_invite/zt-xhqp2m4i-JOCaN1vRN2NDXSVif10aQg">Community forum</a>
    </h3>
</div>


# What is Embeddinghub?

[Embeddinghub](https://docs.featureform.com/) is a database built for machine learning embeddings. It is built with four goals in mind.

* Store embeddings durably and with high availability
* Allow for approximate nearest neighbor operations
* Enable other operations like partitioning, sub-indices, and averaging
* Manage versioning, access control, and rollbacks painlessly

<br />
<br />

<img src="docs/assets/embeddinghub.png" alt="drawing" style="width:35em"/>

<br />
<br />


## Features
* **Supported Operations**: Run approximate nearest neighbor lookups, average multiple embeddings, partition tables (spaces), cache locally while training, and more.
* **Storage**: Store and index billions vectors embeddings from our storage layer.
* **Versioning**: Create, manage, and rollback different versions of your embeddings.
* **Access Control**: Encode different business logic and user management directly into Embeddinghub.
* **Monitoring**: Keep track of how embeddings are being used, latency, throughput, and feature drift over time.

<br />


## What is an Embedding?

Embeddings are dense numerical representations of real-world objects and relationships, expressed as a vector. The vector space quantifies the semantic similarity between categories. Embedding vectors that are close to each other are considered similar. Sometimes, they are used directly for “Similar items to this” section in an e-commerce store. Other times, embeddings are passed to other models. In those cases, the model can share learnings across similar items rather than treating them as two completely unique categories, as is the case with one-hot encodings. For this reason, embeddings can be used to accurately represent sparse data like clickstreams, text, and e-commerce purchases as features to downstream models.

### Further Reading
* [Read up on common embeddings use cases, like recommender systems, nearest neighbor, and natural language processing in our docs.](https://docs.featureform.com)
* [The Definitive Guide to Embeddings](https://www.featureform.com/post/the-definitive-guide-to-embeddings)

<br />
<br />

# Getting Started

## Step 1: Install Embeddinghub client

Install the Python SDK via pip

```
pip install embeddinghub
```

## Step 2: Deploy Docker container ( _optional_ )
The Embeddinghub client can be used without a server. This is useful when using embeddings in a research environment where a database server is not necessary. If that’s the case for you, skip ahead to the next step.

Otherwise, we can use this docker command to run Embeddinghub locally and to map the container's main port to our host's port.

```
docker run featureformcom/embeddinghub -p 7462:7462
```

## Step 3: Initialize Python Client

If you deployed a docker container, you can initialize the python client.

```py
import embeddinghub as eh

hub = eh.connect(eh.Config())
```
Otherwise, you can use a LocalConfig to store and index embeddings locally.

```py
hub = eh.connect(eh.LocalConfig("data/"))
```

## Step 4: Create a Space

Embeddings are written and retrieved from Spaces. When creating a Space we must also specify a version, otherwise a default version is used.

```py
space = hub.create_space("quickstart", dims=3)
```

## Step 5: Upload Embeddings
We will create a dictionary of three embeddings and upload them to our new quickstart space.

```py
embeddings = {
    "apple": [1, 0, 0],
    "orange": [1, 1, 0],
    "potato": [0, 1, 0],
    "chicken": [-1, -1, 0],
}
space.multiset(embeddings)
```

## Step 6: Get nearest neighbors

Now we can compare apples to oranges and get the nearest neighbors.

```py
neighbors = space.nearest_neighbors(key="apple", num=2)
print(neighbors)
```

* [Read through our guide to further explore Embeddinghub’s functionality.](https://docs.featureform.com)
* [Explore our docs](https://docs.featureform.com/)

<br />

# Contributing

* To contribute to Embeddinghub, please check out [Contribution docs](https://github.com/featureform/embeddings/blob/main/CONTRIBUTING.md).
* Welcome to our awesome community, please join our [Slack community](https://join.slack.com/t/featureform-community/shared_invite/zt-xhqp2m4i-JOCaN1vRN2NDXSVif10aQg).

<br />


# Report Issues

Please help us by [reporting any issues](https://github.com/featureform/embeddings/issues/new/choose) you may have while using Embeddinghub.

<br />

# License

* [Mozilla Public License Version 2.0](https://github.com/featureform/embeddings/blob/main/LICENSE)
