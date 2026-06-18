# Stampede Risk Detection using Motion Analysis, Crowd Density Estimation, and Multimodal Risk Fusion
This project presents an AI-based stampede risk detection system designed to identify potentially dangerous crowd situations before a stampede occurs. The system combines motion analysis and crowd density estimation to evaluate risk in real time.
Traditional crowd monitoring often relies heavily on human observation, which becomes unreliable in large-scale events such as concerts, religious gatherings, festivals, stadiums, and public celebrations. This project addresses that challenge by using deep learning to automatically detect abnormal crowd motion, estimate crowd density, and generate a unified risk score indicating the likelihood of stampede formation.
The system is designed for public safety monitoring, smart surveillance, crowd management, and emergency response systems.


## Dataset Sources
This project uses multiple crowd analysis datasets:
### Crowd Motion Dataset
Abnormal crowd behavior videos containing normal and abnormal high-density crowd movement:
* Times Square crowd footage
* Italy crowd surveillance footage
* Crowd Activity dataset
### Crowd Density Dataset
ShanghaiTech Crowd Counting Dataset:
* Part A
* Part B
These datasets provide both motion-based abnormal crowd patterns and crowd density ground truth annotations.


## Preprocessing
### Motion Analysis Pipeline
* Video frames extracted from crowd surveillance footage
* Optical Flow generated using Farneback algorithm
* Flow frames resized to **300 × 300**
* Sequence creation using **5 consecutive frames**
* Dataset labeled into:
  * NORMAL
  * ABNORMAL
### Crowd Density Pipeline
* Ground-truth annotations converted into density maps
* Gaussian kernel density generation
* Random patch cropping
* Input resized to **384 × 384**


## Model Architecture
### Motion Detection Model
A hybrid CNN-LSTM architecture was developed for temporal crowd behavior analysis.
**Backbone CNN:** EfficientNet-B0
**Temporal Module:** LSTM
Pipeline:
* EfficientNet-B0 extracts spatial features from optical flow frames
* LSTM learns temporal crowd movement patterns
* Final dense layers classify:
  * NORMAL
  * ABNORMAL
### Crowd Density Estimation Model
A lightweight CSRNet-inspired architecture was developed for density estimation.
Architecture:
* Convolutional frontend for feature extraction
* Dilated convolution backend for density regression
* Density map generation
* Crowd count estimation
This model predicts spatial crowd density maps and total crowd counts.
## Multimodal Risk Fusion
Final stampede risk is computed by combining:
* Motion abnormality score
* Crowd density score
Fusion equation:
Risk Score = α × Motion Score + β × Density Score
Where:
* α = 0.6
* β = 0.4
Risk levels:
* LOW
* MEDIUM
* HIGH
This fusion allows robust risk estimation by incorporating both behavioral and spatial crowd information.


## Results
Model evaluation outputs including confusion matrix, ROC curve, risk heatmaps, and sample predictions are available in the repository **results** folder.
### Motion Detection Performance
* Binary Classification: NORMAL vs ABNORMAL
* Metrics:
  * Accuracy
  * Precision
  * Recall
  * F1 Score
  * ROC-AUC
### Crowd Density Performance
Metrics used:
* MAE (Mean Absolute Error)
* RMSE (Root Mean Squared Error)
### Generated Outputs
* Confusion Matrix
* Classification Report
* ROC Curve
* Risk Score Timeline
* Spatial Risk Heatmaps
* Overlay Heatmaps on Crowd Frames


## Backend / API
A FastAPI backend was developed to serve the trained AI models.
Capabilities:
* Accept crowd video input
* Perform motion analysis
* Perform density estimation
* Compute fused risk score
* Return risk prediction and visualization outputs
This enables deployment as a real-time surveillance API.


## Frontend
A web-based frontend was developed to interact with the FastAPI backend.
Features:
* Upload crowd surveillance videos
* Real-time risk visualization
* Display heatmaps
* Risk level alerts (LOW / MEDIUM / HIGH)
* Prediction analytics dashboard
This interface enables easier usage for safety operators and crowd management teams.


## Project Workflow
1. Video acquisition from surveillance feeds
2. Optical flow generation
3. Motion classification using CNN-LSTM
4. Crowd density estimation using CSRNet
5. Multimodal risk fusion
6. Risk score generation
7. Heatmap visualization and alert generation


## Skills Demonstrated
* Computer Vision
* Deep Learning
* Optical Flow Analysis
* CNN-LSTM
* Crowd Counting
* Density Map Generation
* FastAPI Deployment
* Risk Scoring Systems
* End-to-End AI Pipeline Development


## Note
Training code, backend implementation, and frontend source code are not included in this repository because the research work has been submitted to an IEEE conference for peer review.
This repository is intended to showcase the project methodology, architecture, evaluation results, and research contributions.


## Publication Status
Research paper submitted to an IEEE Conference ICETCE 2026 and currently under review.
