## About ImageMesh

ImageMesh is a visual explorer application that allows interactive visualisation of a dataset of images drawn from the [arXiv](https://arxiv.org/) repository. This version uses 600,000 images from a total of over 12 million in the arXiv bulk dataset up to July 2020.

[ArXiv](https://arxiv.org/) is a repository that maintains over 1.5 million preprint articles across a diverse range of scientific fields. It provides access to metadata and bulk source data downloads. While this data has been widely examined, it has not been used, to our knowledge, to investigate the images that contribute to the fields of scientific research represented such as astrophysics, computer vision, and high energy physics, to name only a few.

ImageMesh draws inspiration from [imgs.ai](https://imgs.ai/), developed by Fabian Offert, with contributions by Peter Bell and Oleg Harlamov. It has been developed as a mode of encountering the practical and conceptual research conducted by [Anna Munster](https://research.unsw.edu.au/people/professor-anna-marie-munster), Professor of Media Arts and Theory, University of New South Wales, [Adrian MacKenzie](https://researchers.anu.edu.au/researchers/mackenzie-a), Professor of Sociology, Australian National University and Dr. [Kynan Tan](https://kynantan.com/), postdoctoral fellow on this project. The project underpinning its development, ‘Re-imaging the empirical: statistical visualisation in art and science’ was supported by funding from the Australian Research Council, Discovery Project scheme. More information about this project can be found [here](https://github.com/re-imaging/re-imaging).

## Screencast

A short video demonstrating the use of ImageMesh and highlighting some of the key features.

https://player.vimeo.com/video/561663847

## Compatibility

Please note that ImageMesh may not render correctly on mobile devices. Desktop platforms are preferred. Requires a modern browser e.g. Firefox or Chrome.

## Running searches

The dataset can be searched either by randomly sampling the dataset or by pulling the nearest neighbours to a target image according to a particular machine learning embedding. Toggle the radio buttons to choose the search mode. If using the nearest neighbours search, you are required to select an image by double clicking on one from the grid. Searching will then bring up the nearest neighbours to that image according to that embedding. The selected image has no effect on random sampling.

In addition to the search mode, the results can be filtered according to the metadata of the image, paper, and associated caption. The archive and category (subject area) can be selected using the dropdown menus. The keyword search will find matches across all metadata fields. Click on the optional filters button to see additional filters. Many filters provide suggestions of the top results, while some filters require typing a keyword, such as title, caption, or abstract.

## Embeddings

There are five embeddings currently available. Each embedding is created by using a particular neural network to process each image in the dataset and then saving the resulting data. This data was further reduced using Principal Component Analysis, we used the [scikit-learn IncrementalPCA](https://scikit-learn.org/stable/modules/generated/sklearn.decomposition.IncrementalPCA.html). The reduced data was then used to construct a nearest neighbours map using the [Annoy library](https://github.com/spotify/annoy), which allows for fast approximate k-nearest neighbours over large sets of data. The machine learning embeddings are pre-computed, meaning that the nearest neighbour search is fast and computationally cheap. This enables exploration of the dataset using the images themselves to bring up different ‘slices’ of the dataset according the way different neural networks interpret the image data.

### - ternary

This classifier was trained using manually labelled images. The researchers labelled 9748 randomly sampled images from arXiv as either diagram, sensor, or mixed. Sensor refers to images that appear to have been captured using photography or other capture devices. This classifier was then trained on these images and achieved accuracy of 92.07% on the cross-validation dataset. While the classifier has learned features of the images, due to the small number of training samples there are a number of strange results produced when run over the larger subset of data.

### - VGG16

The VGG16 architecture, pre-trained on ImageNet. We used the [Keras](https://keras.io/) implementation. This classifier achieves high accuracy on ImageNet. Using this embedding is more likely to produce associations based on image classification, such as detecting a particular object in the image, due to the large quantities of data used in pre-training. Note also that the top-5 predictions using VGG16 have been saved in the metadata and can be accessed via hovering over the selected image.

### - raw

The raw pixels of each image. Generally produces associations based on overall colour content.

### - cats

A classifier trained on images of cats and dogs. We used keras to train this network, following [this example](https://keras.io/examples/vision/image_classification_from_scratch/). Produces some unlikely associations between images.

### - DeepCluster

We used the method of unsupervised learning outlined in the arXiv paper [Deep Clustering for Unsupervised Learning of Visual Features](https://arxiv.org/abs/1807.05520) to train a classifier that predicts whether images belong to 100 different clusters. This produces strong similarity among particular image trends, e.g. logos, schematics, photographs, graphs showing small multiples. This provides the highest degree of learning based on the arXiv images dataset. For more details on the code used, see the [DeepCluster GitHub](https://github.com/facebookresearch/deepcluster).

## Data Policy

We do not record or store any data from users.
