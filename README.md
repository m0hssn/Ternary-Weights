# CIFAR-10 Image Classification with Ternary Weight Transformation
This project implements a simple Convolutional Neural Network (CNN) for classifying images from the CIFAR-10 dataset. The model is designed to reduce its size by transforming its weights into a ternary format (-1, 0, 1) using a custom tanh transformation. The impact of this transformation on model accuracy is evaluated as part of the training process.

## Custom Weight Transformation

The custom transformation method is designed to convert the model's weights into a ternary format with values of -1, 0, and 1. This is done through the following steps:

1. **Ternary Transformation Function**: A modified version of the standard tanh function is applied to the model weights. This function outputs values in the set \{-1, 0, 1\} based on predefined thresholds:
   - If the tanh output is greater than 0.666, the value is set to 1.
   - If the tanh output is less than -0.666, the value is set to -1.
   - If the tanh output is within the range of [-0.666, 0.666], the value is set to 0.

   The formula is:

$$
   f(x) = 
   \begin{cases} 
   1 & \text{if } \tanh(x) > 0.666 \\
   0 & \text{if } -0.666 \leq \tanh(x) \leq 0.666 \\
   -1 & \text{if } \tanh(x) < -0.666 
   \end{cases}
$$


2. **Weight Transformation Application**: During this step, each weight in the model is transformed based on the ternary transformation function. Additionally, the weights are normalized by dividing by their mean absolute value (`γ`) to ensure proper scaling:

  $$
   \hat{w} = \text{f}\left(\frac{w}{\gamma + \epsilon}\right)
  $$
  
   Where:
   - $w$ is the original weight.
   - $\gamma$ is the mean absolute value of the weight.
   - $\epsilon$ is equal to $1e-7$

This transformation aims to reduce the model's size and complexity while retaining as much performance as possible by approximating the original weights with the ternary values -1, 0, and 1.

## Results
After training the model on the CIFAR-10 dataset, the following results were obtained:

- Accuracy before applying weight transformation: 70.88%
- Accuracy after applying weight transformation: 55.02%
- Change in accuracy after applying transformation: -15.86%

This transformation successfully reduces the model's size by simplifying the weights to ternary values. Despite the notable drop in accuracy (from 70.88% to 55.02%), this trade-off is valuable in scenarios where model compression is critical. The substantial size reduction, achieved with a relatively small loss in accuracy, demonstrates the effectiveness of this approach in balancing performance and efficiency.

  
These results indicate a significant drop in accuracy after the ternary transformation, highlighting the trade-off between model size reduction and predictive performance.










