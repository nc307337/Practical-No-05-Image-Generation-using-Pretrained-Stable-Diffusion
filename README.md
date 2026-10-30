# Practical-No-05-Image-Generation-using-Pretrained-Stable-Diffusion

from pathlib import Path

readme = r"""# Practical 05: Image Generation Using Pretrained Stable Diffusion

## Aim
To implement a pretrained Stable Diffusion model using the Hugging Face Diffusers library to generate images from text prompts and study the effect of:
1. Number of inference steps
2. Guidance scale
3. Sampling methods (schedulers)

## Requirements
- Google Colab (recommended)
- GPU runtime: T4 GPU or another compatible CUDA GPU
- Python
- Internet connection for downloading the pretrained model

## Libraries Used
- `torch`
- `diffusers`
- `transformers`
- `accelerate`
- `safetensors`
- `matplotlib`
- `time` (Python standard library)

## Installation
Run the following commands in a Colab code cell:

```python
!pip uninstall -y torchao
!pip install -q -U diffusers transformers accelerate safetensors
```

If Colab asks you to restart the runtime after installation, restart it and run the notebook cells again from the beginning.

## Pretrained Model
The notebook uses the Stable Diffusion v1.5 model from Hugging Face:

`stable-diffusion-v1-5/stable-diffusion-v1-5`

The pipeline is loaded with `torch.float16` precision and moved to the available device. A GPU is recommended because the model is large and image generation is significantly slower on CPU.

## Implementation Overview

### 1. Import libraries
The notebook imports PyTorch, Matplotlib, timing utilities, the Stable Diffusion pipeline, and five scheduler classes:
- PNDM
- DDIM
- Euler
- Euler Ancestral
- DPM Solver Multistep

### 2. Load the pretrained pipeline
The code checks whether CUDA is available, loads the pretrained Stable Diffusion v1.5 pipeline, moves it to the selected device, and stores the default scheduler configuration for later experiments.

### 3. Image generation function
The `generate()` function accepts:
- `prompt`: text description of the required image
- `steps`: number of inference/denoising steps (default: 30)
- `guidance`: classifier-free guidance scale (default: 7.5)
- `seed`: random seed (default: 42)

It generates one image and returns the image and elapsed generation time. A fixed seed helps make comparisons more consistent.

### 4. Image display function
The `show_images()` function displays multiple generated images in a grid with titles.

## Experiments

### Experiment 1: Basic text-to-image generation
The prompt used in the notebook is:

> A futuristic humanoid AI robot standing in a modern smart city, glowing blue eyes, advanced technology, beautiful skyscrapers, cinematic lighting, ultra realistic, highly detailed, 4K

The model generates an image from this text prompt and prints the time taken.

### Experiment 2: Effect of inference steps
The notebook tests the following inference-step values:

`[5, 10, 20, 30, 50]`

The scheduler is kept fixed as DPM Solver Multistep and the guidance scale remains 7.5. Only the number of steps changes.

**Expected observation from the notebook comments:**
- Very few steps (for example, 5) can produce a rough or unfinished image.
- Image quality generally improves as the number of steps increases.
- Around 20–30 steps, visual improvement may become smaller while generation time continues to increase.

### Experiment 3: Effect of guidance scale
The notebook tests these guidance values:

`[1, 3, 7.5, 15, 30]`

The number of steps remains 30 and the scheduler remains DPM Solver Multistep. Only the guidance scale changes.

**Expected observation from the notebook comments:**
- A very low guidance scale may not follow the prompt closely.
- Around 7–10 can provide a useful balance between prompt adherence and image quality.
- A very high value (such as 30) may cause over-contrasted or distorted images.

### Experiment 4: Effect of sampling method
The notebook compares five schedulers while keeping the prompt, inference steps (30), guidance scale (7.5), and seed fixed:

| Sampling method | Scheduler |
|---|---|
| PNDM | `PNDMScheduler` |
| DDIM | `DDIMScheduler` |
| Euler | `EulerDiscreteScheduler` |
| Euler Ancestral | `EulerAncestralDiscreteScheduler` |
| DPM++ 2M | `DPMSolverMultistepScheduler` |

**Expected observation from the notebook comments:**
- Different schedulers can produce differences in image appearance and sampling behaviour.
- Euler Ancestral can produce a different result because it adds stochastic noise during sampling.
- Generation times may be similar because the neural network denoising computation is the main cost.

## Conclusion
This practical demonstrates text-to-image generation using a pretrained Stable Diffusion v1.5 model and Hugging Face Diffusers.

1. Increasing inference steps can improve image quality, but also increases generation time. The notebook suggests that improvements may become smaller after approximately 20–30 steps.
2. Guidance scale controls how strongly the generated image follows the text prompt. The notebook identifies approximately 7–10 as a useful balance; very high values may distort the image.
3. Different schedulers change the sampling process and can affect image appearance and generation behaviour.
4. The notebook's suggested starting configuration is DPM++ 2M, 25–30 inference steps, and a guidance scale of 7–8.

**Note:** The observations above are the qualitative expectations documented in the notebook. Actual images and timings depend on the runtime, GPU, library versions, and execution. Run the notebook and include your own generated outputs and measured timings in the practical report.

## How to Run
1. Open the `.ipynb` notebook in Google Colab.
2. Select **Runtime → Change runtime type → T4 GPU** (or another available GPU).
3. Run the installation cell.
4. Restart the runtime if requested.
5. Run the remaining cells in order.
6. Review the generated images and execution times for all four experiments.

## Project Files
- `Practical No05 Image Generation using Pretrained Stable Diffusion.ipynb` — implementation and experiment code.
- `README.md` — project overview, setup instructions, experiment descriptions, and conclusion.
"""

out = Path("/mnt/data/README.md")
out.write_text(readme, encoding="utf-8")
print(f"Created: {out}")
