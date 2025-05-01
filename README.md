# Indoor Object Detection and Safety Zone Classification

This project focuses on detecting indoor objects (e.g., tables, chairs, chandeliers) and classifying safe and unsafe areas based on predefined rules. It integrates object detection and safety zone classification to enable automated analysis of indoor environments. I believe that this project will help people who dont know where to cover when an earthquake hits.

---

## Table of Contents
1. [Overview](#overview)
2. [Features](#features)
3. [Dataset Structure](#dataset-structure)
4. [Pipeline](#pipeline)
5. [Installation](#installation)
6. [Usage](#usage)
7. [Future Work](#future-work)
8. [Contributing](#contributing)
9. [License](#license)

---

## Overview
The goal of this project is to:
1. Train a model to detect indoor objects using a large dataset.
2. Generate safety zones based on object types (e.g., "under table = safe", "under chandelier = unsafe").
3. Calculate distances between safe and unsafe zones and reclassify zones if safety constraints are violated.

This project can be applied in areas like indoor safety assessments, robotics navigation, and disaster preparedness.

---

## Features
1. **Object Detection**:
   - Detects objects such as tables, desks, chandeliers, windows, and more using YOLOv5.
   
2. **Safety Zone Classification**:
   - Defines safe zones under sturdy objects (e.g., tables, desks).
   - Marks unsafe zones near hazardous objects (e.g., chandeliers, fans).

3. **Distance-Based Safety Constraints**:
   - Calculates distances between zones and ensures safe zones are sufficiently far from unsafe zones.
   - Reclassifies zones if constraints are violated.

4. **Modular Pipeline**:
   - Easily extendable for new object categories or safety rules.

---

## Dataset Structure
The project uses two types of datasets:
1. **Indoor Object Detection Dataset**:
   - Contains labeled indoor objects like tables, desks, chandeliers.
2. **Safety Zone Annotations**:
   - Manually annotated zones for safe and unsafe areas.

### Example Dataset Structure
```
datasets/
├── train/
│   ├── images/
│   ├── labels/
│   ├── annotations.json
├── val/
│   ├── images/
│   ├── labels/
│   ├── annotations.json
```

### Unified Class Labels
Classes include:
- Safe Objects: `table`, `desk`
- Unsafe Objects: `chandelier`, `fan`, `window`

---

## Pipeline
1. **Object Detection**:
   - Train YOLOv5 on the indoor object detection dataset.
   - Use the model to detect objects in input images.

2. **Zone Creation**:
   - Generate zones based on detected objects.
   - Label zones as `safe` or `unsafe` based on predefined rules.

3. **Distance Computation**:
   - Calculate distances between safe and unsafe zones.
   - Apply constraints to ensure safe zones are sufficiently far from unsafe zones.

4. **Visualization**:
   - Visualize detected objects and safety zones on input images.

---

## Installation
1. Clone the repository:
   ```bash
   git clone https://github.com/yigitgrit/indoor-object-detection.git
   cd indoor-object-detection
   ```

2. Install dependencies:
   ```bash
   pip install -r requirements.txt
   ```

3. Download pretrained YOLOv5 weights:
   ```bash
   wget https://github.com/ultralytics/yolov5/releases/download/v5.0/yolov5s.pt
   ```

---

## Usage
### Training the Model
1. Combine datasets and prepare the unified dataset structure.
2. Train YOLOv5:
   ```bash
   python train.py --img 640 --batch 16 --epochs 50 --data combined_data.yaml --weights yolov5s.pt --name indoor_objects
   ```

### Running the Pipeline
1. Detect objects:
   ```bash
   python detect.py --weights runs/train/indoor_objects/weights/best.pt --source input_image.jpg
   ```

2. Generate safety zones and apply constraints:
   ```bash
   python main_pipeline.py --input input_image.jpg --output output_image.jpg
   ```

### Visualizing Results
Output images with labeled safety zones will be saved in the specified output directory.

---

## Future Work
- Add support for more object categories.
- Automate safety zone annotation using 3D point clouds.
- Extend the pipeline to analyze video feeds for real-time safety assessments.

---

## Contributing
Contributions are welcome! Please follow these steps:
1. Fork the repository.
2. Create a new branch: `git checkout -b feature-name`.
3. Commit your changes: `git commit -m "Add new feature"`.
4. Push to the branch: `git push origin feature-name`.
5. Submit a pull request.

---

## License
This project is licensed under the MIT License. See the [LICENSE](LICENSE) file for details.
