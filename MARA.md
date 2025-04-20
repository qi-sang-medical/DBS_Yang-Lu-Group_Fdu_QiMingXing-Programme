## 1. Introduction: What is MARA? (EEGLAB)

**MARA** (Multiple Artifact Rejection Algorithm) is an automatic, machine learning-based method for classifying and removing artifact components from independent components (ICs) obtained via ICA decomposition of EEG data. It is widely used in the EEGLAB toolbox to objectively and efficiently identify ICs related to eye movement, muscle, heart, and other non-neural artifacts.

---

## 2. Principle and Workflow

MARA works by extracting a set of discriminative features from each IC, then applies a **Linear Discriminant Analysis (LDA)** classifier previously trained on expert-labeled data to distinguish "brain" from "artifact" components.

### **Step-by-Step Algorithmic Process**

#### **A) Feature Extraction**

For each IC, MARA computes six features, capturing:

- **Spectral Properties:**  
  (e.g., relative power in high vs. low frequencies; distinguishes EMG/muscle from brain activity)
- **Spatial Properties:**  
  (e.g., how spatially focal the IC-projection is; helps with blink and EOG artifact identification)
- **Temporal Properties:**  
  (e.g., kurtosis, skewness, time-series predictability; identifies abrupt, non-neural events)

#### **B) Feature Normalization**

Each feature $x_i​ $is z-scored:

$$
z_i = \frac{x_i - \mu_i}{\sigma_i}


$$

where $μ_i$​ and $σ_i​ $are the mean and standard deviation for feature i, derived from the training set.

#### **C) Linear Discriminant Analysis (LDA) Classifier**

Each IC's normalized feature vector z is scored as:

$$
s_i = \mathbf{w}^{T}\mathbf{z}_i+b
$$

Where:

- w: Weight vector (trained on labeled data)
- z: The 6-dimensional feature vector (normalized)
- b: Bias term

#### **D) Classification**

If s>threshold, the component is classified as an artifact; otherwise, as a brain component.

---

## 3. Model Training (LDA Derivation, Summarized)

MARA's LDA classifier is parameterized with weights and bias found by maximizing separation between two classes ("artifact" vs. "brain") in the feature space:

w=Σ−1(μ1​−μ0​)

- Σ: Common within-class covariance matrix
- μ1​,μ0​: Feature means of artifact and brain classes, respectively

The threshold and bias are set using class priors and means so as to optimize accuracy.

---

## 4. Pseudocode

for each IC in ICA_results:
    features = extract_features(IC)                               # Extract 6 features
    features_z = (features - mean) / std                       # Normalize features
    score = np.dot(weights, features_z) + bias            # LDA score
    if score > threshold:
        label = 'Artifact'
    else:
        label = 'Brain'
    return label

---

## 5. Formal Summary (with Formula)

For a set of N ICs:

$$
IC_i: \mathbf{z}_i \rightarrow s_i = \mathbf{w}^{T}\mathbf{z}_i + b

$$

Classification rule:

$$
\text{label}_i =
\begin{cases}
    \text{“artifact”}, & \text{if } s_i > \tau \\
    \text{“brain”},    & \text{otherwise}
\end{cases}
$$

---

## 6. Reference

- Winkler, I., et al. (2011). "Automatic Classification of Artifactual ICA-Components for Artifact Removal in EEG Signals." **Behavioral and Brain Functions, 7, 30.**  
  [Full Text](https://behavioralandbrainfunctions.biomedcentral.com/articles/10.1186/1744-9081-7-30)

---

## 7. Summary

**MARA in EEGLAB is an automated ICA component classifier based on supervised machine learning (LDA).**  
It represents each IC using a small set of interpretable features, learns to separate artifacts from brain activity using expert training data, and applies the learned decision boundary to new data for fast, objective artifact rejection.
