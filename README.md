# BasketLiDAR: The First LiDAR–Camera Multimodal Dataset for Professional Basketball MOT

**BasketLiDAR** is a multimodal dataset pairing synchronized LiDAR point clouds with RGB cameras in professional basketball scenes, designed for Multi-Object Tracking (MOT) research.  
It includes data, baseline notebooks, and standardized evaluation to facilitate reproducible experiments for LiDAR-only and camera–LiDAR fusion tracking.

> **Paper:** The project paper will be released in **November 2025**.  
> <!--※TODO: 論文公開後に実URLへ置き換えてください → [Details here](#)>

---

## Table of Contents
- [Data Visualization](#data-visualization)
- [Setup](#setup)
- [Datasets](#datasets)
  - [Downloads](#downloads)
  - [Folder Structure](#folder-structure)
- [LiDAR-based Tracking](#lidar-based-tracking)
- [Camera-Fusion Tracking](#camera-fusion-tracking)
- [License](#license)
- [Contact](#contact)

---

## Data Visualization
<!--※OPTIONAL: カメラ画像とLiDAR（BEVや点群）のタイリング映像・静止画を追加してください。  
推奨パス例:
- `assets/visualizations/tiled_demo.mp4`（GitHub のプレビュー対策として `tiled_demo.gif` を併用）
- `assets/visualizations/pc_overview_1.png`
- `assets/visualizations/pc_overview_2.png`

例（画像を追加した場合）:

![Tiled demo](assets/visualizations/tiled_demo.gif)
-->

![dataset preview](visualizations/Fig1_data.png)

---

## Setup

We recommend using a **conda** environment.

### Linux / macOS / Git Bash

```bash
# Create and activate a fresh environment
conda create -n basketlidar python=3.11 -y
conda activate basketlidar

# Install dependencies (requirements.txt is provided at the project root)
pip install -r requirements.txt
```

### Windows (PowerShell)

```powershell
conda create -n basketlidar python=3.11 -y
conda activate basketlidar

conda basketlidar update -f environment.yml
```

## Datasets

### Downloads

Access to the dataset is granted upon request for research purposes.

- Please **contact us** with your name, affiliation, and intended use.  
  ※ (#contact)

- Once approved, we will share a **Google Drive link** for download.

> Downloading and usage imply agreement with the dataset terms of use.  
> Redistribution is not allowed without permission.

```

Expected directory layout:

```text
D:.
└─dataset
    ├─frames_img
    │  ├─far-end
    │  │  ├─camera1
    │  │  │  ├─day1_measurement3_scene_camera_frame_02524-02832
    │  │  │  ├─day1_measurement3_scene_camera_frame_03649-04042
    │  │  │  ├─day1_measurement3_scene_camera_frame_16273-16688
    |  |  |  ...
    │  │  ├─camera2
    │  │  │  ├─day1_measurement3_scene_camera_frame_02524-02832
    │  │  │  ├─day1_measurement3_scene_camera_frame_03649-04042
    │  │  │  ├─day1_measurement3_scene_camera_frame_07798-08274
    |  |  |  ...
    │  │  ├─camera3
    │  │  │  ├─day1_measurement3_scene_camera_frame_02524-02832
    │  │  │  ├─day1_measurement3_scene_camera_frame_03649-04042
    │  │  │  ├─day1_measurement3_scene_camera_frame_15075-15389
    |  |  |  ...
    │  │  └─lidar
    │  │      ├─day1_measurement3_scene_camera_frame_02524-02832
    │  │      ├─day1_measurement3_scene_camera_frame_03649-04042
    │  │      ├─day1_measurement3_scene_camera_frame_07798-08274
    |  |      ...
    │  └─near-end
    │      ├─camera1
    │      │  ├─day1_measurement1_scene_camera_frame_00523-01000
    │      │  ├─day1_measurement1_scene_camera_frame_02262-02493
    │      │  ├─day1_measurement1_scene_camera_frame_06815-07138
    |      |  ...
    │      ├─camera3
    │      │  ├─day1_measurement1_scene_camera_frame_00523-01000
    │      │  ├─day1_measurement1_scene_camera_frame_06815-07138
    │      │  ├─day1_measurement1_scene_camera_frame_02262-02493
    |      |  ...
    │      ├─lidar
    │      │  ├─day1_measurement1_scene_camera_frame_00523-01000
    │      │  ├─day1_measurement1_scene_camera_frame_02262-02493
    │      │  ├─day1_measurement1_scene_camera_frame_06815-07138
    |      |  ...
    │      └─camera2
    │          ├─day1_measurement1_scene_camera_frame_11757-12355
    │          ├─day1_measurement1_scene_camera_frame_06815-07138
    │          ├─day1_measurement1_scene_camera_frame_00523-01000
    |          ...
    ├─gt_json
    │  ├─near_end
    │  └─far_end
    ├─pointcloud
    └─lidar_extrinsics
```

<!-- ※TODO: 必要であれば、実際の `tree` 出力に置き換えてください。-->
---

## LiDAR-based Tracking

<!-- ※OPTIONAL: LiDARのみのトラッキング結果を示す動画（例: `assets/visualizations/lidar_tracking_demo.mp4`）やGIFを追加してください。-->
![tracking preview](visualizations/lidar_only.mp4)

This section describes the LiDAR-based tracking pipeline included in the BasketLiDAR dataset.  
It consists of two major steps, both implemented as Jupyter notebooks.

### 1. From raw LiDAR data to BEV detections

The notebook **`pointcloud_to_BEV-detection.ipynb`** demonstrates how to process raw `.lvx2` point cloud files into a bird’s-eye-view (BEV) representation and generate object detection labels.  
This includes:
- Reading `.lvx2` point cloud data  
- Converting point clouds into BEV maps  
- Applying detection models to produce labeled bounding boxes  

If you need more information about the `.lvx2` file structure, please refer to the **official LVX2 format specification** (https://terra-1-g.djicdn.com/65c028cd298f4669a7f0e40e50ba1131/LVX2%20Specifications.pdf).  

### 2. From BEV detections to tracking results

The notebook **`BEV-detection_to_track.ipynb`** takes the detection labels generated in the previous step as input and produces multi-object tracking results.  
This step links detections across frames to maintain object identities over time.  
A detailed step-by-step manual for the tracking configuration and evaluation will be added in future updates.

---

## Camera–Fusion Tracking

<!-- ※OPTIONAL: 融合トラッキング結果の動画やGIFを `assets/visualizations/cam_fusion_demo.mp4` として追加してください。-->

The notebook **`camfusion_postprocess.ipynb`** demonstrates how to perform tracking-by-fusion using both LiDAR and camera information.  
This post-processing step refines LiDAR-based tracks by incorporating visual cues from synchronized RGB frames, improving object continuity and identity preservation.  
As with the LiDAR-based pipeline, a more detailed explanation and reproducibility guide will be released progressively.


## License
 <!-- ※TODO: 正式なライセンスを明記（例: Code: MIT / Data: Custom Research License）-->

### Code License

All source code in this repository is released under the **MIT License**.  
See the [LICENSE](./LICENSE) file for details.

### Dataset License

The dataset (including LiDAR point clouds, camera images, and annotations)  
is released **for research and educational purposes only** under the following terms:

- Redistribution, rehosting, or public sharing of the dataset, in whole or in part, is **strictly prohibited** without explicit permission from the authors.  
- You may use the dataset internally for **non-commercial research** and **academic publications**.  
- When publishing results based on this dataset, please **cite the corresponding paper** once it becomes available.

> **Summary:**  
> - ✅ Code → MIT License  
> - 🚫 Data → Research use only / Redistribution prohibited

---

## Contact
Questions, requests, or collaborations are welcome.

- Overview and Dataset request: https://sites.google.com/keio.jp/keio-csg/projects/basket-lidar
- Email: **hayashi.ryu430@keio.jp**  
- Issues: Please open a GitHub issue with a clear title and description.
