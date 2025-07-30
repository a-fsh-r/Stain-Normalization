## 🎨 Stain Normalization (Modified Reinhard)

In histopathological image analysis, **color variation** is a critical issue caused by inconsistent staining protocols and differences between scanners. These color shifts can reduce the performance and generalization of deep learning models.

To mitigate this, we applied **stain normalization** using the **Modified Reinhard method**, implemented via the [`LBBNorm`](https://pypi.org/project/LBBNorm/) library. This preprocessing step aligns the color distribution of all images to a selected reference image, ensuring more consistent and robust training data for CNN-based cancer detection.

### ✅ Benefits

- Reduces color inconsistencies across histology slides  
- Makes training data more uniform  
- Improves **model robustness** and **generalization**, especially in cross-institutional datasets  
- Enhances reproducibility of medical image analysis workflows

### 📦 Installation

```bash
pip install LBBNorm Pillow numpy

### 🧪 How It Works

The **Modified Reinhard** method matches the mean and standard deviation of each channel (in Lab color space) between a target image and a reference image. Unlike traditional Reinhard, this version is better suited for histology images where tissue structure matters.

---

### 🧱 Example Usage

```python
from LBBNorm import ModifiedReinhard
from PIL import Image
import numpy as np

# Load image and reference image
img = Image.open("path/to/image.png")
ref = Image.open("path/to/reference_image.png")

# Convert to numpy arrays
img_np = np.array(img)
ref_np = np.array(ref)

# Apply Modified Reinhard normalization
normalized_img = ModifiedReinhard(img_np, ref_np)

# Save normalized image
Image.fromarray(normalized_img).save("normalized_image.png")
