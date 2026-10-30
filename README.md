Practical No. 05 – Image Generation Using Pretrained Stable Diffusion
1. Project Overview
This project implements a pretrained Stable Diffusion model using the Hugging Face Diffusers library to generate images from text prompts.

It also analyzes how different inference steps, guidance scales, and sampling methods affect the quality and generation time of images.
2. Aim
To implement a pretrained Stable Diffusion model using the Hugging Face Diffusers library for text-to-image generation and study the impact of:
- Inference steps
- Guidance scale
- Different sampling methods (Schedulers)
3. Technologies Used
- Python
- Google Colab
- PyTorch
- Hugging Face Diffusers
- Stable Diffusion v1.5
- Transformers
- Matplotlib
- CUDA GPU
4. Requirements
- Google Colab account
- T4 GPU or compatible GPU
- Python 3
- Internet connection
- Hugging Face Diffusers library
5. Installation
Run the following command in Google Colab:
!pip install -q -U diffusers transformers accelerate safetensors



6. Pretrained Model
The project uses the Stable Diffusion v1.5 pretrained model from Hugging Face.

Model ID:

stable-diffusion-v1-5/stable-diffusion-v1-5

The model converts a text prompt into an image using a diffusion-based image generation process.
7. Project Implementation
Experiment 1: Basic Text-to-Image Generation
A text prompt is provided to the pretrained Stable Diffusion model to generate an image.

Example Prompt:

"A futuristic humanoid AI robot standing in a modern smart city, glowing blue eyes, advanced technology, beautiful skyscrapers, cinematic lighting, ultra realistic, highly detailed, 4K."

Expected Output: A generated AI robot image based on the given prompt.
Experiment 2: Effect of Inference Steps
Inference steps represent the number of denoising iterations used to generate an image.

Values tested:

[5, 10, 20, 30, 50]

Observation:
- 5 steps: Image may appear rough.
- 10 steps: Image structure improves.
- 20 steps: Better image details.
- 30 steps: Good quality image.
- 50 steps: More processing time, with potentially smaller quality improvements.
Conclusion: Increasing inference steps can improve image quality but also increases generation time.
Experiment 3: Effect of Guidance Scale
Guidance scale controls how closely the generated image follows the given text prompt.

Values tested:

[1, 3, 7.5, 15, 30]

Observation:
- 1: Weak prompt influence.
- 3: Moderate prompt influence.
- 7.5: Balanced image generation.
- 15: Strong prompt influence.
- 30: May produce over-contrasted or distorted images.
Conclusion: A guidance scale around 7–10 can provide a useful balance between prompt matching and image quality.
Experiment 4: Comparison of Sampling Methods
Different schedulers are used to compare image generation quality and processing time.

Sampling methods:
Sampling Method	Scheduler
PNDM	PNDMScheduler
DDIM	DDIMScheduler
Euler	EulerDiscreteScheduler
Euler Ancestral	EulerAncestralDiscreteScheduler
DPM Solver	DPMSolverMultistepScheduler

Observation:
- PNDM uses pseudo numerical methods for denoising.
- DDIM provides an alternative sampling process.
- Euler can produce detailed images.
- Euler Ancestral introduces stochastic variation.
- DPM Solver is designed for efficient image generation.
Conclusion: Different sampling methods can produce different image characteristics and generation times.
8. How to Run the Project
1. Open the Jupyter Notebook in Google Colab.
2. Select Runtime → Change runtime type.
3. Select T4 GPU.
4. Install the required Python libraries.
5. Import the required libraries.
6. Load the pretrained Stable Diffusion model.
7. Execute the image generation function.
8. Run all four experiments.
9. Compare the generated images and execution times.
9. Results
The project generates images from text prompts using Stable Diffusion.

The experiments help compare:
- Image quality at different inference steps.
- Prompt matching at different guidance scales.
- Image appearance and generation time with different schedulers.
Add your actual generated image screenshots and measured execution times here after running the notebook.
10. Conclusion
This practical successfully demonstrates text-to-image generation using a pretrained Stable Diffusion model and the Hugging Face Diffusers library.

The experiments show that inference steps, guidance scale, and sampling methods influence the image generation process.

Increasing inference steps can improve image details but requires more time. Guidance scale controls prompt adherence, while different schedulers can affect image appearance and generation speed.

A useful starting configuration is:
- Inference Steps: 30
- Guidance Scale: 7.5
- Sampling Method: DPM Solver
11. Future Scope
- Generate high-resolution images.
- Experiment with different pretrained diffusion models.
- Use negative prompts to improve generated images.
- Build a web application for text-to-image generation.
- Compare additional sampling schedulers.
12. References
- Hugging Face Diffusers Documentation
- Stable Diffusion v1.5 Model
- PyTorch Documentation

Project: Image Generation Using Pretrained Stable Diffusion

Practical No.: 05

Programming Language: Python

Platform: Google Colab

Author: Nilesh Raju Chavan

Branch: Computer Science and Engineering (AI & ML)
