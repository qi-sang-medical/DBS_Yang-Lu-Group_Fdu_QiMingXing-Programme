## DBS Project Introduction

---

## The project is still in progress. This is only a draft version.

---

#### Basic Information

This research is sponsored by FDU Xi_De College as a training and enlightening programme for freshmen and sophomores, led by Prof Yang Lu.

Five participants are as follows：

| Name        | Major             | Contact                    |
| ----------- | ----------------- | -------------------------- |
| YanHong Jin | Life Science      | 23307090071@m.fudan.edu.cn |
| RuiQi Liu   | Clinical Medicine | 24301050114@m.fudan.edu.cn |
| ZiYuan Wang | Clinical Medicine | 24301050288@m.fufan.edu.cn |
| HaoYu Zhang | Life Science      | 23307110387@m.fudan.edu.cn |
| ZiHeng Zhou | Life Science      | 24307110092@m.fudan.edu.cn |

#### Background

The transformation between explicit learning and implicit learning has always been an important topic in cognitive neuroscience. Building upon the research conducted by Prof. Yang Lu’s team (submitted for review but not yet published, and therefore cannot be fully disclosed due to academic ethics), this project specifically investigates the representation of the posterior occipital lobe in implicit learning and its relationship with the representation of the prefrontal lobe in implicit learning, thereby verifying that “the posterior occipital lobe is a key brain region in the transformation from explicit learning to implicit learning.”

- Reber, A. S. (1993). Implicit learning and tacit knowledge: An essay on the cognitive unconscious. Oxford University Press.

- Fletcher, P. C., & Henson, R. N. (2001). Frontal lobes and human memory: Insights from functional neuroimaging. *Brain*, 124(5), 849–881.
  
  https://doi.org/10.1093/brain/124.5.849

#### Experimental design

to be completed

#### Data processing

| No.  | Main Steps                          | Core Methods & Tools                                     | Main Advantages                                              |
| ---- | ----------------------------------- | -------------------------------------------------------- | ------------------------------------------------------------ |
| 1    | Behavioral Data Preprocessing       | Python (pandas, numpy, scipy, statsmodels)               | Performs descriptive statistics, t-tests, and variance analyses to quickly reveal response differences under various conditions |
| 2    | EEG Data Preprocessing              | EEGLAB (MATLAB scripts)                                  | Efficient batch processing, filtering, ICA artifact removal, rereferencing, ensuring data quality needed for subsequent source localization |
| 3    | Source Localization & MVPA Analysis | Python–MNE, MVPA (SlidingEstimator, Logistic Regression) | Uses dSPM source localization and temporal decoding to quantitatively assess the effects of cTBS on neural regulation during implicit and explicit learning stages |

###### Behavioral evidence

###### Neural evidence

EEG preprocessing

```mermaid
flowchart LR  
A["Load Data"] --> B["Assemble Electrode Coordinates"]  
B --> C["Filtering"]  
C --> D["Downsampling"]  
D --> E["Segmentation"]  
E --> F["Bad Channel Detection"]  
F --> G["Re‑referencing"]  
G --> H["ICA Preparation & Execution"]
```

