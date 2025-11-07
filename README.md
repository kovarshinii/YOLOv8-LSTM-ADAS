# YOLOv8-LSTM-ADAS
YOLOv8-LSTM based hybrid predictive cut-in forward collision warning in ADAS

Forward collision warning systems in modern ADAS primarily rely on single-frame analysis, lacking the temporal context necessary for accurate predictive capabilities. Traditional methods often generate false positives or miss imminent collisions due to their inability to model vehicle dynamics and trajectory patterns over time.

This research presents a hybrid deep learning framework combining YOLOv8 object detection with Long Short-Term Memory (LSTM) networks for predictive Cut-in forward collision warning in Advanced Driver Assistance Systems (ADAS). The system processes temporal sequences of driving scenes to anticipate potential collisions, addressing critical limitations of traditional single-frame analysis methods. By extracting spatiotemporal features from consecutive frames and learning temporal dependencies. This approach achieves early warning capabilities with 89.2% accuracy and 0.934 ROC AUC, significantly outperforming conventional computer vision methods. The proposed system demonstrates robust performance on the Car Crash Dataset, providing real-time collision probability estimates with visual warnings for enhanced road safety.

Hybrid Architecture: 

First integration of YOLOv8 with LSTM for temporal collision prediction ||
Temporal Understanding: Sequence-based analysis instead of single-frame processing ||
Real-time Performance: Optimized for practical ADAS deployment ||
Comprehensive Evaluation: Extensive ablation studies and performance benchmarking

Key Innovations:

Sequential feature extraction from object detection outputs
Temporal pattern learning using LSTM networks
Multi-frame collision probability estimation
Real-time visualization with warning thresholds

System Architecture 

Input Frames → YOLOv8 Detection → Feature Extraction → LSTM Sequence Processing → Cut in collision Prediction → Visual Warning

Module Functions

Module 1: 

YOLOv8 Object Detection
Function: Real-time vehicle detection and localization
Input: RGB frames (640×640 resolution)
Output: Bounding boxes, confidence scores, class labels
Classes: Cars, trucks, buses, motorcycles
Key Features:
Real-time processing (>30 FPS)
Multi-class vehicle detection
Bounding box regression

Module 2: 

Feature Extraction Engine
Function: Convert detections to temporal features
Features Extracted:
Normalized bounding box coordinates (center_x, center_y)
Vehicle dimensions (width, height, area)
Motion features (approximated velocity)
Spatial context (in_center, near_bottom flags)
Detection confidence scores

Module 3:

LSTM Temporal Processor
Function: Learn temporal patterns from feature sequences
Architecture:
Input: 30 features × 5 frames sequence
Layers: 2 LSTM layers (64→32 units)
Regularization: Dropout (0.3-0.4), L2 regularization
Output: Collision probability (0-1)

Module 4: 

Collision Warning System
Function: Generate real-time warnings
Thresholds:
SAFE: Probability < 0.3 (Green)
WARNING: 0.3 ≤ Probability < 0.7 (Orange)
CRASH IMMINENT: Probability ≥ 0.7 (Red)

Dataset Description : 

Car Crash Dataset 

Total Images: 10,000 annotated frames
Classes: Collision (1,993), Non-collision (8,007)
Annotations: Binary labels (collision: 'y'/'n')
Image Resolution: Various resolutions, standardized to 640×640
Sequence Creation: Synthetic sequences of 5 frames for temporal analysis

Output Formats:

Visual Warnings: Color-coded bounding boxes and text alerts
Probability Scores: Continuous collision likelihood (0-1)
Log Files: Timestamped predictions and system status
Performance Metrics: Accuracy, precision, recall, F1-score

Key Results Analysis

Early Detection: System predicts collisions 3-5 frames earlier than single-frame methods
False Positive Reduction: 42% reduction compared to YOLO-only approach
Context Awareness: Better handling of occlusions and complex scenarios

Architecture Performance:

YOLOv8-LSTM (Ours): 89.2% accuracy
CNN-LSTM Hybrid: 84.7% accuracy
Bidirectional LSTM: 82.3% accuracy
GRU Model: 80.1% accuracy
Dense Baseline: 76.8% accuracy

Feature Importance Analysis:

Vehicle Vertical Position (0.184) - Proximity to ego vehicle
Bounding Box Area (0.162) - Vehicle size and distance
Horizontal Position (0.148) - Lane positioning
Detection Confidence (0.135) - Detection reliability
Near Bottom Flag (0.121) - Immediate collision risk

Strengths of Proposed System: 

Temporal Intelligence: Understands vehicle dynamics over time ||
Early Warning: Predicts collisions before they become imminent ||
Robust Performance: Handles various lighting and weather conditions ||
Interpretable Features: Clear feature importance for validation ||
Scalable Architecture: Adaptable to different vehicle types and scenarios.
