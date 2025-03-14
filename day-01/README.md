Learn ComfyUI - Day 1: Introduction to ComfyUI (Updated)
What is ComfyUI?
ComfyUI is a node-based interface for Stable Diffusion that allows for creating complex image generation workflows. Unlike other Stable Diffusion interfaces, ComfyUI gives you granular control through a visual programming approach using nodes and connections.
Day 1 Goals

Understand what ComfyUI is and why it's useful
Install ComfyUI on your system (local or cloud)
Get familiar with the basic interface
Create your first simple image generation workflow

Installation Options
Local Installation
To install ComfyUI locally:

Make sure you have Python 3.10 or newer installed
Clone the ComfyUI repository:
Copygit clone https://github.com/comfyanonymous/ComfyUI
cd ComfyUI

Install the required dependencies:
Copypip install -r requirements.txt

Download a Stable Diffusion model (like SD 1.5) and place it in the models/checkpoints folder
Run ComfyUI:
Copypython main.py

Open your browser and navigate to http://localhost:8188

Cloud Installation Options
Google Colab

Open a new Google Colab notebook
Paste and run the following code:
pythonCopy!git clone https://github.com/comfyanonymous/ComfyUI
%cd ComfyUI
!pip install -r requirements.txt

# Download a model (SD 1.5 in this example)
!mkdir -p models/checkpoints
!wget -O models/checkpoints/v1-5-pruned-emaonly.safetensors https://huggingface.co/runwayml/stable-diffusion-v1-5/resolve/main/v1-5-pruned-emaonly.safetensors

# Start ComfyUI and create a tunnel with ngrok or cloudflared
!pip install pyngrok
from pyngrok import ngrok
!python main.py --listen &
public_url = ngrok.connect(8188)
print(f"ComfyUI is available at: {public_url}")


RunPod/Vast.ai

Create a new instance with a GPU (RTX 3090, A100, etc.)
Choose a Stable Diffusion template if available
Once connected to the instance via SSH or web terminal:
bashCopygit clone https://github.com/comfyanonymous/ComfyUI
cd ComfyUI
pip install -r requirements.txt

# Download a model
mkdir -p models/checkpoints
wget -O models/checkpoints/v1-5-pruned-emaonly.safetensors https://huggingface.co/runwayml/stable-diffusion-v1-5/resolve/main/v1-5-pruned-emaonly.safetensors

# Start ComfyUI with public access
python main.py --listen

Access ComfyUI via the public URL provided by your cloud provider

Paperspace/Gradient

Create a new Notebook with a GPU
Choose PyTorch runtime
Run the following commands:
bashCopy!git clone https://github.com/comfyanonymous/ComfyUI
%cd ComfyUI
!pip install -r requirements.txt

# Download a model
!mkdir -p models/checkpoints
!wget -O models/checkpoints/v1-5-pruned-emaonly.safetensors https://huggingface.co/runwayml/stable-diffusion-v1-5/resolve/main/v1-5-pruned-emaonly.safetensors

# Start ComfyUI
!python main.py --listen

Look for the public URL in the output

Basic Interface Overview

Canvas: The main workspace where you'll create your node workflows
Node Menu: Right-click on the canvas to access the node browser
Properties Panel: View and edit the properties of selected nodes
Queue: Manages the processing of your workflows

Your First Workflow
Let's create a basic image generation workflow:

Right-click on the canvas and add a "KSampler" node
Add a "CLIPTextEncode" node (this will be your prompt)
Add another "CLIPTextEncode" node (for your negative prompt)
Add a "CheckpointLoaderSimple" node to load your model
Add an "EmptyLatentImage" node to set your canvas size
Add a "VAEDecode" node to convert the latent image to a viewable image
Add a "SaveImage" node to save your creation

Connect the nodes:

CheckpointLoaderSimple → model input on KSampler
First CLIPTextEncode (positive prompt) → positive input on KSampler
Second CLIPTextEncode (negative prompt) → negative input on KSampler
EmptyLatentImage → latent_image input on KSampler
KSampler output → VAEDecode input
VAEDecode output → SaveImage input

Enter a prompt like "a beautiful landscape, mountains, lake, sunset, highly detailed" in your positive prompt node, and "blurry, bad quality, deformed" in your negative prompt.
Set your EmptyLatentImage to 512x512 resolution.
Click the "Queue Prompt" button to generate your first image!
Cloud-Specific Tips

When using cloud platforms, always save your workflows using the "Save (API Format)" option to download them locally
For Colab, be aware that your session will eventually timeout, so save your work regularly
For paid platforms like RunPod, remember to shut down your instance when not in use to avoid unnecessary charges
Consider setting up a persistent storage solution for your models and outputs

Next Steps
For Day 2, we'll explore more about ComfyUI's sampling methods and parameters, and how they affect your generated images.