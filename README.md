# Master Thesis – D3DP & PSTMO: Combined Model Implementation

This repository contains a combined and modified implementation of the following 3D human pose estimation models, as part of my Master's Thesis:

- [D3DP (Diffusion-driven 3D Pose)](https://github.com/paTRICK-swk/D3DP)
- [P-STMO (Progressive Spatio-Temporal Motion Offsets)](https://github.com/paTRICK-swk/P-STMO)
- [video-to-pose3D](https://github.com/zh-plus/video-to-pose3D) – used for extracting 2D keypoints from input videos.

> ⚠️ Please refer to the README of the original repositories to understand the complete folder structure, weights, and model usage. However, **use the code provided in this repository**, as it has been modified to suit this combined implementation.

---

## 📁 Folder Structure

```
.
├── video-to-pose3D-D3DP/                  # Contains modified code from zh-plus/video-to-pose3D for D3DP
│   │   └── outputs/                       # Place input videos here for D3DP

├── video-to-pose3D-PSTO/                  # Contains modified code from zh-plus/video-to-pose3D for PSTMO
│       └── outputs/                       # Place input videos here for PSTMO
├── Data/                                  # Final 3D pose outputs and intermediate results
│   └── Ground Truth/                      # Ground truth files go here (for evaluation)

├── Calculate_Angles                       # Script to compute joint angles from 3D keypoints
├── Calculate_MPJAE                        # Script to compute MPJAE metric
└── .gitattributes                         # Git LFS tracking for large files
```

---

## 🚀 How to Run

### Step 1: Add Your Input Videos

- For **D3DP**, put videos inside:  
  `Data/D3DP/outputs/`

- For **P-STMO**, put videos inside:  
  `Data/PSTMO/outputs/`

---

### Step 2: Run the Main Scripts

Each script runs a complete pipeline:
- Extract 2D keypoints using a modified video-to-pose3D implementation
- Feed them to the model
- Save 2D and 3D outputs

#### ▶️ For D3DP:
```bash
python video-to-pose3D-D3DP/videopose_diffusion.py
```

#### ▶️ For PSTMO:
```bash
python video-to-pose3D-PSTO/videopose_PSTMO.py
```

---

## 📤 Output Format

Each run will generate:

- `xxx_2D.npz`: 2D keypoints stored inside  
  `<ModelName>/outputs/<VideoName>/`

- `xxx_3D.npy`: 3D keypoints stored in the same directory

---

## 📐 Evaluation Scripts

- Execute `Calculate_Angles.py` to compute various angles.
   - The results are saved directly in the Data folder.
   - Individual Action Files: For each action, an individual file is created that contains the computed angles.
   - Consolidated Files: Two consolidated files are created:
   - Ground_Truth_Angles_Processed/Model_Angles_Processed: Contains data processed from Model's output, where the first frame's data has been subtracted from the rest of the frames in each action sequence to reduce initial bias.
   - Ground_Truth_Angles/Model_Angles: Absolute Angles.

  - Run `Calculate_MPJAE.py` to calculate the Mean Per Joint Angle Error (MPJAE) between ground truth and Model's predicted results. You can choose whether you want to use processed angles or absolute angles and modify the code accordingly (For thesis I used processed angles). The output will be stored in the Data folder in Excel format.
 
  - **NOTE**: Both models share a similar flow.

---

## 🧠 Credits

This implementation combines and modifies components from:

- [paTRICK-swk/D3DP](https://github.com/paTRICK-swk/D3DP)
- [paTRICK-swk/P-STMO](https://github.com/paTRICK-swk/P-STMO)
- [zh-plus/video-to-pose3D](https://github.com/zh-plus/video-to-pose3D)

---

## 📄 License

This code is for academic and research use only. Please refer to the original repositories for licensing terms.
