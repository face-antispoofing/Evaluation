# The metric
The HTER metric, which is defined as
$$
HTER=\frac{FAR+FRR}{2}
$$
Where
- <b>FAR</b> (False Acceptance Rate) represents the probability that a system incorrectly verifies an unauthorized user (system accepts an impostor).
- <b>FRR</b> (False Rejection Rate) represens the probability that the system incorrectly rejects an authorized user (systems denies access wrongly)

# Results
| **Model** | **HTER** |
|------------|----------|
| Original CNN                          | 0.57875 |
| Deep CNN 1                            | 0.31500 |
| Deep CNN 2                            | 0.38375 |
| Alexnet with CrossEntropyLoss         | 0.53125 |
| Deep CNN 1 with tuned learning rate   | 0.28250 |

## Notes on the models and preprocessing
Train and test/val datasets are using different types of transformations with the training one having more transformations done to the pictures.

Original CNN	                        -   The given custom CNN model given in Pytorch_demo.ipynb, a simple CNN architecture.
Deep CNN 1	                            -   Based on the given CNN model with more layers. Convolutions are done with kernel_size=3 and padding=1, while MaxPool's are done with kernel_size=2 and stride=2. At the end of convolution, the tensor has 2048 different channels.
Deep CNN 2	                            -   A custom CNN architecture which utilizes many dropout layers in the convolution. Convolution goes only up until 128 different channels. (Original architecture: https://medium.com/@mayankverma05032001/binary-classification-using-convolution-neural-network-cnn-model-6e35cdf5bdbb).
Alexnet with CrossEntropyLoss           -   An Alexnet CNN architecture but using CrossEntropyLoss (Softmax) instead of a Sigmoid activation function.
Deep CNN 1 with tuned learning rate	    -   Deep CNN 1 model, however the learning rates were fine tuned using ray tune with tune.loguniform(1e-4, 1e-1) where the HTER was minimized.
