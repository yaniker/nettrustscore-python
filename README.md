# NetTrustScore - NTS

This repository provides a Python implementation of trustworthiness quantification metrics for predictive models (e.g., DNNs) as proposed in [How Much Can We Really Trust You? Towards Simple, Interpretable Trust Quantification Metrics for Deep Neural Networks](https://arxiv.org/pdf/2009.05835). The metrics evaluate a model's trustworthiness based on its confidence behavior in correct and incorrect predictions.  

###
**The implementation is flexible and works out-the-box with any Python code that outputs SoftMax probabilities.**
###

### Key Features
- **Question-Answer Trust**: Computes trust scores per sample based on prediction correctness and softmax probability.
- **Trust Density**: Estimates the distribution of trust scores per class using Kernel Density Estimation (KDE).
- **Trust Spectrum**: Visualizes trust densities across all classes.
- **NetTrustScore (NTS)**: Provides a scalar metric summarizing overall trustworthiness.

---

## Installation
### Recommended: Install via Conda-Forge
The easiest way to install nettrustscore is via Conda-Forge, which handles all dependencies automatically. Run the following command:
```bash
conda install -c conda-forge nettrustscore
```

### Alternative: Manual Installation
If you prefer to install the package manually or are not using Conda, you can install the required dependencies and clone the repository.

Install Dependencies
- **NumPy**: For numerical calculations.
- **Matplotlib**: For plotting the trust spectrum.
- **Scikit-learn**: For Kernel Density Estimation (KDE) in trust density estimation.

Install them via pip:

```bash
pip install numpy matplotlib scikit-learn
```

or

Install them via conda:

```bash
conda install numpy matplotlib scikit-learn
```

Clone the Repository
```bash
git clone https://github.com/yaniker/nettrustscore-python.git
cd nettrustscore-python
```

## Example Usage
```python
from trustquant import NTS, CNTS #This is how the package is imported.
import numpy as np

# Example oracle and predictions
oracle = np.array([0, 0, 1, 2, 2, 0, 1])  # True labels
predictions = np.array([
    [0.8, 0.1, 0.1],  # Correct, high confidence
    [1.0, 0.0, 0.0],  # Correct, high confidence
    [0.2, 0.7, 0.1],  # Correct, high confidence
    [0.1, 0.2, 0.7],  # Correct, high confidence
    [0.1, 0.4, 0.5],  # Correct, lower confidence
    [0.1, 0.8, 0.1],  # Incorrect, high confidence
    [0.3, 0.3, 0.4]   # Incorrect, low confidence
]
) #Replace this with your model's predictions (`predictions = model.predict()`)

# FOR NETTRUSTSCORE #
# Initialize with default parameters
nts = NTS(oracle, predictions) #This is how you initialize. trust_spectrum = True will save trust spectrum to the directory under "trust_spectrum.png"
nts_scores_dict = nts.compute() # Computes trustworthiness for each class and overall.

# FOR CONDITIONAL NETTRUSTSCORE #
# Initialize with default parameters
cnts = CNTS(oracle, predictions) #This is how you initialize. trust_spectrum = True will save trust spectrum to the directory under "trust_spectrum.png" and "conditional_trust_densities.png"
cnts_scores_dict = cnts.compute() # Computes trustworthiness for each class and overall.

```

Example Plot for Trust Spectrum (`trust_spectrum = True`)
![Alt text](./assets/trust_spectrum.png)

Example Plot for Conditional Trust Spectrum (`trust_spectrum = True`)
![Alt text](./assets/conditional_trust_densities.png)

## This code was developed as a part of my publications listed below:  
1. Yanik, E., Kruger, U., Intes, X., Rahul, R., & De, S. (2023). Video-based formative and summative assessment of surgical tasks using deep learning. Scientific Reports, 13(1), 1038.
2. Yanik, E., Ainam, J. P., Fu, Y., Schwaitzberg, S., Cavuoto, L., & De, S. (2024). Video-based skill acquisition assessment in laparoscopic surgery using deep learning. Global Surgical Education-Journal of the Association for Surgical Education, 3(1), 26.
3. Yanik, E., Schwaitzberg, S., Yang, G., Intes, X., Norfleet, J., Hackett, M., & De, S. (2024). One-shot skill assessment in high-stakes domains with limited data via meta learning. Computers in Biology and Medicine, 174, 108470. / Yanik, E., Schwaitzberg, S., Yang, J., Intes, X., & De, S. (2022). One-shot domain adaptation in video-based assessment of surgical skills. arXiv e-prints, arXiv-2301.
4. Yanik, E., Intes, X., & De, S. (2024). Cognitive-Motor Integration in Assessing Bimanual Motor Skills. arXiv preprint arXiv:2404.10889.
5. Ainam, J. P., Yanik, E., Rahul, R., Kunkes, T., Cavuoto, L., Clemency, B., ... & De, S. (2024). Deep Learning for Video-Based Assessment of Endotracheal Intubation Skills. arXiv preprint arXiv:2404.11727.

## Licence
This project is licensed under the MIT License. See the  file for details.

## If you use this package in your research, please cite the following paper:

```
@article{wong2020much,
  title={How much can we really trust you? towards simple, interpretable trust quantification metrics for deep neural networks},
  author={Wong, Alexander and Wang, Xiao Yu and Hryniowski, Andrew},
  journal={arXiv preprint arXiv:2009.05835},
  year={2020}
}
```
