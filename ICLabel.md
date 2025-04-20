# 1. What is ICLabel? (EEGLAB)

**ICLabel** is a fully-automated algorithm for classifying Independent Components (ICs) from EEG datasets using machine learning. Integrated into EEGLAB, ICLabel leverages a large, crowd-sourced training set and deep learning, providing probabilistic multi-class classification for each IC (brain, muscle, eye, heart, line noise, channel noise, other).

---

# 2. Principle and Workflow

## Overview

- **Input:** Scalp maps, power spectra, autocorrelation functions, and more for each IC
- **Model:** Trained deep neural networks (DNNs, multiple MLPs)
- **Output:** For each IC, probabilities for 7 classes (sum to 1):
    - **brain**
    - **muscle**
    - **eye**
    - **heart**
    - **line noise**
    - **channel noise**
    - **other**

**Set of classes:**

C={brain, muscle, eye, heart, line noise, channel noise, other}

---

# 3. Machine Learning Algorithm: Derivation & Structure

## A. Feature Extraction

- **Scalp map:** 2D topography of IC
- **Power spectrum:** Frequency features
- **Autocorrelation:** Time pattern features
- **Other:** Temporal/contextual features

These features are extracted for each IC and fed as model inputs.

## B. Model Architecture

- **Parallel MLPs** for each feature type (e.g., for scalp map, spectrum...), outputs concatenated
- Then, dense layers combine features and produce output
- Final layer: **softmax** for class probabilities

**Formally:**  
Let $x$= IC’s feature tensor

### Subnetwork representations:

$$
h_k = f_k(x_k)
$$
### Combine and transform:
$$
z = g\left( \mathrm{concat}(h_1, h_2, \ldots) \right)
$$
### Softmax for output classes:
$$p_c = \frac{\exp(z_c)}{\sum_{j=1}^7 \exp(z_j)}$$

## C. Model Training

### Loss function: (Categorical cross-entropy)

$$L = -\sum_{c=1}^7 y_c \log p_c$$
---

# 4. Classification Workflow: Pseudocode
```python
for each IC in ICA_results:
    features = extract_features(IC)    # scalp map, spectrum, autocorr, etc.
    class_probs = ICLabel_NN(features) # neural net, outputs 7 probabilities
    top_class = argmax(class_probs)    # class with max probability
    confidence = class_probs[top_class]
    assign_label(IC, top_class, confidence)
```



# 5. Example Formula

For one IC with features $x$:

$$p_c = \frac{\exp(f_c(x))}{\sum_{j=1}^7 \exp(f_j(x))}$$

where $p_c$​ is the probability of class $c$.

---

# 6. Official Reference

Pion-Tonachini, L., Kreutz-Delgado, K., & Makeig, S. (2019).  
ICLabel: An automated electroencephalographic independent component classifier, dataset, and website.  
**NeuroImage, 198, 181–197.**  
[[Full Paper]](https://www.sciencedirect.com/science/article/pii/S1053811919304185)  
##### [[ICLabel website]](https://iclabel.ucsd.edu/)
---

# 7. Summary & Comparison with MARA

- **ICLabel:**
    - Multi-class
    - Deep learning (DNN)
    - Probabilistic classification
    - Richer feature sets
- **MARA:**
    - Binary classification (brain/artifact)
    - Linear discriminant analysis
    - Handcrafted features

ICLabel is now the default, recommended IC classifier in EEGLAB.