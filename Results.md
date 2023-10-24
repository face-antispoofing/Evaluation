# The metric
We are evaluating using the HTER metric, which is defined as
$$
HTER=\frac{FAR+FRR}{2}
$$
Where
- <b>FAR</b> (False Acceptance Rate) represents the probability that a system incorrectly verifies an unauthorized user (system accepts an impostor).
- <b>FRR</b> (False Rejection Rate) represens the probability that the system incorrectly rejects an authorized user (systems denies access wrongly)

# Results
| **Model** | **HTER** |
|------------|----------|
| [1] | 0.5562 |
| [2] | 0.5063 |
| [3] | 0.3838 |
| [4] | 0.5025 |
| [5] | 0.4413 |
| [6] | 0.4175 |
| [7] | 0.4138 |
| [8] | 0.5425 |
| [9] | 0.4200 |
| [10] | 0.5225 |
| [11] | 0.500 |
| [12] | 0.500 |
| [13] | 0.4950 |
| [14] | 0.3788 |
| [15] | 0.4988 |
| [16] | 0.4725 |
| [17] | 0.4175 |
| [18] | 0.4800 |
| [19] | 0.5000 |
| [20] | 0.5487 |
| [21] | 0.5100 |
| [22] | 0.3650 |

## Notes on the models
- [1] (as-is) notebook. The model is overfitting quite a lot. The model is able to reach 100% train accuracy after 8 epochs
- [2] introduces RandomHorizontalFlip(p=0.5)
- [3] introduces RandomResizedCrop(size=(224, 224), scale=(0.08, 1.0)) plus transformations from model [2]
- [4] introduces RandomAffine(degrees=10, translate=(0.1, 0.1), scale=(0.9, 1.1)) plus transformations from model [3]
- [5] introduces RandomErasing(p=0.5, scale=(0.02, 0.33), ratio=(0.3, 3.3), value='random') plus transformations from model [3]
- [6] introduces RandomErasing(p=0.5, scale=(0.02, 0.1), ratio=(0.3, 3.3), value=0.4) plus transformations from model [3]
- [7] introduces GaussianBlur(kernel_size=(5, 5), sigma=(0.1, 2.0)) plus transformations from model [3]
- [8] introduces ColorJitter(brightness=0.2, contrast=0.2, saturation=0.2, hue=0.1) plus transformations from model [3]
- [9] introduces RandomRotation(degrees=10) (before the crop) plus transformations from model [3]
- [10] doubles the batch size from model (from 16 to 32) [3]
- [11] sets the learning rate to 0.005 (5 times the former learning rate) using model [3] as baseline
- [12] sets the learning rate to 0.01 (10 times the former learning rate) using model [3] as baseline
- [13] sets the learning rate to 0.0001 (one tenth of the former learning rate) using model [3] as baseline. The accuracy is higher than the average.
- [14] introduces the scheduler for the learning rate: StepLR(optimizer, step_size=6, gamma=0.1). Base model is [3]
- [15] introduces the scheduler for the learning rate: StepLR(optimizer, step_size=5, gamma=0.1) and doubles the number of epochs (now 20). Base model is [3]
- [16] introduces a new conv2d+relu+gap. The classifier gets adapted too (256 * 28 * 28 -> 512). Base model is [14]
- [17] uses the GAP instead of the last maxpooling. The classifier gets adapted too (256 * 28 * 28 -> 512). Base model is [14]
- [18] introduces batch_norm after each conv2d and introduces a new classifier layer. Base model is [14]
- [19] the classifier layer has half the neurons (128) and dropout is reduced to 0.3. Base model is [14]
- [20] we introduce a preprocessing: the Viola-Jones face detection. The model overfits quite a lot Base model is [14]
- [21] we introduce batch-normalization to model is [20]. The accuracy is the highest (up to 89% on validation)
- [22] we train our model for 2 epochs only. Learning rate: 0.0005; Step-LR: step_size=1, gamma=0.2; Augmentation: RandomHorizontalFlip, RandomResizedCrop

### Other considerations
- TTA did not improve performances 