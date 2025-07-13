# 📡 SAR Image Enhancement and Terrain Classification Methods
_Deep learning that turns grayscale radar into vivid, actionable maps_
![SAR](./assets/SAR.png)

Synthetic Aperture Radar (SAR) image enhancement and terrain classification are essential for accurate remote sensing analysis. Enhancement techniques, such as speckle noise reduction, histogram equalization, and deep learning-based super-resolution, improve image clarity and feature visibility.

For terrain classification, Convolutional Neural Networks (CNNs) are commonly used to segment and categorize land cover types. When combined with enhancement pipelines, these techniques enable precise mapping for real-world applications in agriculture, disaster response, and environmental monitoring.

## 🚀 Overview
Synthetic Aperture Radar (SAR) is priceless for all‑weather, day‑night Earth observation—but its greyscale intensity images can be tough to interpret. **SARGAN** enhances, colorizes, and classifies SAR data so you see the story hiding in the static.

1. **Enhancement** → Speckle denoising, histogram equalization, super‑resolution  
2. **Colorization** → U‑Net + PatchGAN paints SAR in realistic RGB  
3. **Terrain Classification** → CNN segments land‑cover for agriculture, disaster relief, urban‑growth & more  

---

## 🛠️ Tech Stack
| Layer | Tools |
|-------|-------|
| **Language** | Python 🐍 |
| **Numerics** | NumPy 🔢 |
| **Visualization** | Matplotlib 📊 & OpenCV 👁️ |
| **Deep Learning** | TensorFlow / Keras⭕ |

---

## 🧠 Model Zoo
| Model Variant | What We Tried | One‑Line Verdict |
|---------------|---------------|------------------|
| Simple GAN + **L1** | Vanilla encoder‑decoder | ✅ Crisp edges, ❌ washed‑out colors |
| **L1 + SSIM** | Adds structural loss | Better tones & sharper edges |
| **MSE + L1 + SSIM** | Stabilizes training | Marginal color boost, slower |
| GAN _without_ upsampling | Dense decoder only | 🚨 Total fail on fine detail |
| **U‑Net** + custom loss | SSIM + L1 + perceptual | 💎 Superb edges & contrast |
| U‑Net (conv‑only) | No residual/attention | Good detail, low micro‑contrast |
| **U‑Net + PatchGAN** (🥇 **Final**) | Local realism discriminator | Best mix of color & detail; rock‑solid training |

---

## 🏗️ Final Architecture

- **Generator** — U‑Net with skip connections for global context **plus** local texture  
- **Discriminator** — **PatchGAN**: judges realism on N×N patches for ultra‑sharp results  
- **Custom Loss**  
  - `L1` (pixel fidelity)  
  - **SSIM** (perceptual structure)  
  - *Optional* VGG perceptual loss (semantic similarity)  

---

## 📂 Getting Started

```bash
git clone https://github.com/GitsGoel/SARGAN
cd SARGAN
```

## 🗂️ Dataset

Grab both datasets from [Kaggle](https://www.kaggle.com):

- **SAR Image Colorization Dataset**
- **Sentinel‑1/2 Pairs for Terrain Classification**

### 📁 Directory Structure
Inside the model folder, create the following structure:

```bash
data
├───archive
│   └───v_2
│       ├───agri
│       ├───barrenland
│       ├───grassland
│       └───urban
├───test
│   ├───opt
│   └───sar
└───train
    ├───opt
    └───sar

```
## 🧪 Training

| 📓 Notebook | 🧠 Purpose           | ▶️ Command        |
|-------------|----------------------|------------------|
| `src/GAN-colorization.ipynb` | Train SAR colorization GAN | Open & run |
| `src/classification.ipynb`   | Train terrain classification CNN | Open & run |

> 💡 *Both notebooks are modular—easily adaptable to new datasets or architectures.*

---

## 🚀 Deploy for Inference

```bash
# After training:
cp models/GAN-colorization.keras   server/models/
cp models/classification.keras     server/models/
```

## 🧩 Use Cases
- Land Cover Mapping

- Disaster Assessment

- Agricultural Monitoring

- Urban Growth Analysis

- Environmental Surveillance

## 👨‍💻 Contributors
- Gitansh Goel
- Manik Chauhan 
