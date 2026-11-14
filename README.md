# GhostPixel 🛡️

**Adversarial Image Immunization & AI Edit Protection Platform**

**GhostPixel** is a full-stack web application designed to protect personal photos and digital artwork from unauthorized AI manipulation. The platform applies imperceptible, mathematically optimized pixel perturbations that remain virtually invisible to the human eye while disrupting how generative AI encoders interpret the image.

---

## 🧠 How It Works

Generative image editors (such as Stable Diffusion) process edits by first compressing an input photo into a compact latent representation using a **Variational Autoencoder (VAE) encoder**, and then reconstructing a new image guided by a text prompt.

GhostPixel intercepts this pipeline at the source:
1. **Latent Target Alignment:** It runs gradient-based optimization (Adam) over the input pixels to steer the image's encoded latent representation toward a neutral, flat target.
2. **Visibility Budget ($L_\infty$ Constraint):** Every optimization step clamps pixel shifts within a strict perturbation budget (`eps`), ensuring the protective noise stays imperceptible to human viewers.
3. **Edit Disruption:** When an unauthorized AI editor attempts to modify the immunized photo, its encoder extracts corrupted feature maps—causing the resulting edit to fail, distort, or ignore the original subject[cite: 1, 2].

---

## ✨ Key Features

* **Image Immunization Studio:** Drag-and-drop uploader with automatic center-cropping and resizing to `512×512`, real-time optimization progress tracking, and a before/after comparison slider.
* **Customizable Protection Budget:** Fine-tune the perturbation strength (`eps` from `0.02` subtle to `0.08` strong) and iteration count (`200` to `1,000` steps)[cite: 1, 2].
* **JPEG-Survival Mode:** Integrates differentiable compression simulation inside the optimization loop so protective perturbations withstand standard lossy compression[cite: 2].
* **4-Panel Verification Lab:** Built-in side-by-side testing suite (`1. Original`, `2. Protected`, `3. AI Edit of Original`, `4. AI Edit of Protected`) using deterministic seeds to verify protection before downloading[cite: 2].
* **Lossless PNG Export:** Exports protected images strictly as uncompressed PNGs to preserve high-frequency adversarial noise[cite: 2].

---

## 🛠️ Tech Stack

* **Frontend:** React (Vite), Tailwind CSS
* **Backend:** Python, FastAPI, Uvicorn
* **AI & Vision Engine:** PyTorch, Hugging Face `diffusers` (`stable-diffusion-v1-5/stable-diffusion-v1-5`), `transformers`, `torchvision`, Pillow[cite: 2]

---

## 🚀 Getting Started

### Prerequisites
* **Python 3.10+** (NVIDIA CUDA GPU with ≥ 6GB VRAM recommended for fast optimization; CPU fallback supported)
* **Node.js 18+** & npm

### 1. Clone the Repository
```bash
git clone [https://github.com/your-username/GhostPixel.git](https://github.com/your-username/GhostPixel.git)
cd GhostPixel