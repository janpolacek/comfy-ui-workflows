# ComfyUI Workflows

Local ComfyUI workflows for Qwen Image 2.1.

## Workflows

- `workflows/Qwen-Image-2.1-Text-to-Image.json` — text-to-image generation.
- `workflows/Qwen-Image-2.1-Image-Edit-Optional-References.json` — image editing with up to 10 reference-image inputs. Image 1 is the edit target; image 2 is an optional reference, and image 3 through image 10 are intentionally left empty.

## Required model files

Place these files in the matching ComfyUI model directories:

- `models/diffusion_models/qwen_image_2.1_int8_convrot.safetensors`
- `models/text_encoders/qwen3vl_8b_w4a8.safetensors`
- `models/vae/qwen_image_2.1_vae_bf16.safetensors`

The workflows expect ComfyUI 0.37.0 or newer.

