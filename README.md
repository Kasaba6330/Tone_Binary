# Yorùbá_Tone_Binary Classification Using Perceptron
This project implements a single-layer binary perceptron model to classify Yoruba vowel tokens into one of the language's three distinct tone levels: Low (L), Mid (M), or High (H). The model learns to separate tones using acoustic features derived from fundamental frequency (F0) analysis.

## Data Source and Feature Engineering
The foundational acoustic data for this model was harvested using **Praat**, a professional software for speech analysis. Instances of Yoruba vowels carrying the three level tones were meticulously analyzed to extract their fundamental frequency (F0) contours over time. The resulting F0 values, plotted against time, formed a series of data points for each vowel token.
To create the features used for training (`slope` and `intercept`), the linear trendline for each F0 contour was calculated. This was done by using a line of best fit (y = mx + c) on the (time, F0) data points, a process efficiently handled within a spreadsheet application like **Microsoft Excel**. The slope (m) of this line represents the direction and rate of the F0 change, while the intercept (c) represents the starting F0 value, together providing a compact numerical representation of the tonal gesture.

## Model Overview
The code trains a separate binary perceptron for each tone class using a one-vs-rest strategy. The initial implementation is configured to classify Low ('L') tones versus all others (M and H). The model's weights are initialized to `[0.5, 0.5, 0.5]` and updated via stochastic gradient descent.

## Customization and Usage
**To run the classifier for a specific tone class:**
*   **For Low Tones:** The code is pre-configured (`binr = 1 if label[pos] == 'L' else 0`).
*   **For Mid Tones:** Modify the binary label line to: `binr = 1 if label[pos] == 'M' else 0`.
*   **For High Tones:** Modify the binary label line to: `binr = 1 if label[pos] == 'H' else 0`.

**Hyperparameter Tuning:**
The initial weights (`wt`) and learning rate (`lr = 0.01`) were chosen as a starting point for convergence. These are key hyperparameters that can be adjusted:
*   **Learning Rate (`lr`):** A smaller value leads to slower but potentially more precise convergence, while a larger value speeds up training but risks overshooting the optimal weights. Experiment with values like 0.001, 0.01, or 0.05.
*   **Initial Weights (`wt`):** While often started at 0.5 or small random values, different initializations can be tested to ensure the model converges reliably.
Execute the script after making any desired changes. The output will display the training process epoch-by-epoch and finalize upon perfect convergence, printing the learned weights for the specified tone class.
