# Sequential Development in Federated Learning

## Phase 0: Exploration Phase
There are several open Large Language Models (LLMs) available. Initially, the main focus is to learn how to fine-tune these models for language translation tasks, which is crucial for implementing Federated Learning. Additionally, it's important to identify the most suitable model from an operational perspective for this early stage. <br>
Experiments were conducted with LLaMA 2, mBART, mT5, Helsinki, and Opus models from HuggingFace, and it was found that mT5 delivered the desired outcomes. Initially, using mT5, the Bleu score improved from 7.56 to 11.49. <br>

## Phase 1: FL for Image Classification
Dataset used: CIFAR-10 (https://www.cs.toronto.edu/~kriz/cifar.html) <br>
Model: CNN with 2 convolutional layers <br>
Framework used: Flower <br>

Successfully initiated our exploration into Federated Learning by deploying a small-scale image classification model using the Flower framework. This initial phase focused on establishing robust connections and facilitating parameter exchanges between the server and clients. Moving forward, the plan is to expand the model's complexity and experiment with diverse datasets to enhance its real-world applicability.

Experiments in phase 1: <br>
1. Tweaking the FL rounds count
2. Changing the client count

## Phase 2: FL for Text Classification
Dataset used: IMDB Dataset (https://huggingface.co/datasets/stanfordnlp/imdb) <br>
Model: DistilBert (https://huggingface.co/docs/transformers/en/model_doc/distilbert) <br>

The shift from image to text classification necessitated a key adjustment: moving from analyzing pixel values to tokenizing text. This alteration in the model’s architecture increased the need for computational power. This stage highlighted the transition from visual to textual data, exploring the application of federated learning in text-based scenarios.

## Phase 3: FL for Language Translation
Dataset used: eBible (English to Hindi) (https://github.com/BibleNLP/ebible)
Model: mBART (https://huggingface.co/docs/transformers/en/model_doc/mbart) <br>

The final phase involved implementing Federated Learning for translation tasks. Learnings from the second phase on text-based Federated Learning were instrumental, but numerous adjustments were still necessary. The model selection was crucial; while DistilBert from phase 2 remained unchanged, for translation, the mBART model developed by Facebook was selected due to its suitability for sequence outputs. This required updates to both input and output tokenization.

A significant challenge was the computational demand: DistilBert had 60M-70M parameters, whereas mBART featured around 600M. Transferring such a high volume of parameters was impractical. To address this, a research paper (https://arxiv.org/abs/2007.07779) introducing AdapterHub was consulted. AdapterHub facilitates the simple integration of adapters for efficient fine-tuning of Transformer-based models.

An adapter from AdapterHub (config = "pfeiffer") was integrated with mBART, allowing only the adapter layers’ parameters to be updated and transferred. This strategy reduced the parameter volume from about 600M to 3M (less than 1%), making it feasible to run Federated Learning for translation.

Future Scope: The dataset used was relatively small, the next step involves using larger datasets for real-world applications. However, despite the reduced number of parameters transferred, the high system RAM usage remains a bottleneck that must be addressed before scaling up.

## Federated Learning holds substantial potential for data security applications, and it is exciting to contribute to its development on the scale of a large language model.
