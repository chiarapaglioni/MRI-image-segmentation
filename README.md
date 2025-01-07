### MRI Brain Segmentation Using U-Net (2D and 3D Approaches)

---

#### **Overview**
This repository contains implementations for segmenting different brain regions from MRI scans using deep learning techniques. The task involves segmenting five distinct tissue layers (air, skin/scalp, skull, cerebrospinal fluid (CSF), gray matter, and white matter) from a series of T1-weighted MRI scans. Two approaches are explored:

1. **2D U-Net**: Processes individual slices independently.
2. **3D U-Net**: Leverages spatial information across consecutive slices for improved segmentation.

---

#### **Data Description**
The input data consists of:
- **T1-weighted MRI scans**: A 3D volume of size `(362, 434, 10)` representing 10 consecutive axial slices of the brain.
- **Labels**: Ground truth segmentations for the MRI scans of size `(362, 434, 10)` with region labels:
  - `0`: Air
  - `1`: Skin/Scalp
  - `2`: Skull
  - `3`: CSF
  - `4`: Gray Matter
  - `5`: White Matter

---

#### **Approach**

1. **Preprocessing**:
   - Normalize the input MRI scans to `[0, 1]`.
   - Resize the slices to `(256, 256)` for computational efficiency.
   - Split data into training and test sets.

2. **2D U-Net**:
   - Each slice is treated independently for segmentation.
   - A classical U-Net architecture is used, processing 2D images of shape `(256, 256, 1)`.
   - Output is a segmentation map of the same size, with pixel-wise class probabilities.

3. **3D U-Net**:
   - Processes 3D volumes of shape `(256, 256, 10, 1)`.
   - Leverages spatial context across slices using 3D convolutions.
   - Outputs a 3D segmentation map with voxel-wise class probabilities.

---

#### **Dependencies**
The project runs on Python 3.9.21. The dependencies can be found in the `requirements.txt` and can be installed using `pip`.
   - TensorFlow/Keras
   - NumPy
   - Matplotlib
   - h5py (for `.mat` file handling)

---

#### **Files**
1. **2D U-Net Implementation**:
   - `image-segmentation-2d.ipynb`: Contains the 2D U-Net architecture and training pipeline.
   - Processes each slice independently.

2. **3D U-Net Implementation**:
   - `image-segmentation-3d.ipynb`: Contains the 3D U-Net architecture and training pipeline.
   - Processes 3D volumes for segmentation.

---

#### **Architecture Overview**

- **2D U-Net**:
  - Input: `(256, 256, 1)` (single slice).
  - Encoder-Decoder structure with skip connections.
  - Output: `(256, 256, num_classes)`.

- **3D U-Net**:
  - Input: `(256, 256, 10, 1)` (3D volume).
  - Encoder-Decoder structure using 3D convolutions.
  - Output: `(256, 256, 10, num_classes)`.

---

#### **Key Metrics**
- **Dice Coefficient**:
  - Measures overlap between predicted and ground truth segmentations.
  - High Dice score indicates better segmentation.
