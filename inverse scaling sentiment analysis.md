# Inverse Scaling in Sentiment Analysis

I wanted to see how well conditional generative models could be adapted, without training, to classification tasks. I was inspired by a section in Geoffrey Hinton paper proposing the Forward-Forward algorithm. I find that larger LLMs are worst than smaller ones at identifying sentiment.

## Method
I take a model's loss for each class, *x*, for the prompt "This is an example of *x* text: *example*" In IMDB, the classes are "positive" and "negative." I then invert the losses and put them through the Softmax function to bring them to a normal range. I take the highest valued option and use that as the model's predicted label.

Highlighted is the worst model in each category for accuracy in this kind of IMDB classification.
| Model Type | Model            | Accuracy  |
| ---------- | ---------------- | --------- |
| GPT-Neo    | GPT-Neo-125m     | 68.9%     |
|            | **GPT-Neo-1.3b** | **65.5%** |
| GPT2       | GPT2             | 67.7%     |
|            | GPT2-medium      | 69.9%     |
|            | GPT2-large       | 70.6%     |
|            | **GPT2-xl**      | **58.8%** |
| OPT        | OPT-125m         | 72.8%     |
|            | OPT-350m         | 65%       |
|            | **OPT-1.3b**     | **63.1%** |
|            | OPT-2.7b         | 68.5%     |

Note: These evaluations were done in 16-bit precision, and 32-bit precision may yield a higher accuracy (73.2% instead of 72.8% for OPT-125M was achieved).

This is loosely inspired by a section from the Forward-Forward paper and implemented code on Github that feeds the label of an MNIST image along with the image itself as postive data during training. In inference you can then feed the image along with each potential label, and take the one that maximizes activations at the end.

One can visualize using this same technique with other generative models for example, Stable diffusion's reconstruction loss, to classify data in the domain that the model generates in.

## Why do the larger models perform worse?

> "One explanation of this result is that larger models produce more imitative falsehoods because they are better at learning the training distribution. "

This is an excerpt from the TruthfulQA paper about why larger models generate false data more often than smaller models. Having a low parameter-count sacrifices the precision in which you are able to model incorrect data. Incorrect data is usually a small subset of the training data, and is given less weight in the models.

![Image](https://pbs.twimg.com/media/Fo4REw3WcAQCO_d?format=jpg&name=medium) (a figure from TruthfulQA)
