# ComfyUI Workflows

Curated local ComfyUI workflows for the fictional Red Horizon Mars exploration programme.
The prompts and visual direction are based on [mars-ai-simulation.janpolacek.workers.dev](https://mars-ai-simulation.janpolacek.workers.dev), specifically the published mission records cited below. These are illustrative artworks, not documentary mission imagery.

## Repository layout

- `workflows/` contains loadable ComfyUI workflow JSON files.
- `assets/inputs/pathfinder/` contains copied RH-01 Pathfinder reference images.
- `assets/outputs/` is the designated archive location for generated images and videos. It begins empty except for `.gitkeep`.

## Workflows

### Qwen Image 2.1 — Text to Image

`workflows/Qwen-Image-2.1-Text-to-Image.json`

- **Purpose:** Generate the final approach correction artwork.
- **Prompt source:** `website/news/006-cruise-final-approach.mdx`.
- **Prompt:** A precise, uncrewed course-refinement manoeuvre during interplanetary cruise, with Mars ahead; no astronauts, logos, flags, or text.
- **Inputs:** Text prompt, seed, resolution, and the installed Qwen Image 2.1 weights.
- **Output:** PNG image from the Qwen `Save Image` node.

### Qwen Image 2.1 — Image Edit

`workflows/Qwen-Image-2.1-Image-Edit.json`

- **Purpose:** Render RH-01 Pathfinder leaving its landing site for a measured first traverse.
- **Prompt sources:** `website/news/008-landing.mdx`, `website/news/009-egress.mdx`, and `docs/vehicles/pathfinder/VEHICLE.md`.
- **Inputs:** Pathfinder reference images already selected in the local workflow: `canonical.png`, `front-left.png`, `rear-right.png`, and `contact-arm.png`.
- **Prompt:** A rover moving away from the landing area over natural Mars terrain, with the contact arm retracted, six open-mesh wheels, restrained tracks, and no landing platform, ramp, or human-made landing pad.
- **Output:** PNG image from the Qwen `Save Image` node.

### Wan 2.1 VACE — Pathfinder Multi-Reference Video

`workflows/Wan2.1-VACE-Pathfinder-Multi-Reference-Video.json`

- **Purpose:** Generate a short reference-guided video of a dust-covered RH-01 Pathfinder driving across Asteria Field.
- **Prompt sources:** `website/news/010-health-review.mdx` and `docs/vehicles/pathfinder/VEHICLE.md`.
- **Inputs:** Five Pathfinder views—`canonical.png`, `front-left.png`, `rear-right.png`, `side-view.png`, and `contact-arm.png`—are stitched into a single reference board before reaching `WanVaceToVideo`. The native VACE node accepts one reference-image input, so the board preserves multiple useful viewpoints in that one input.
- **Prompt:** Natural slow rover motion, Mars dust and tracks, with the front contact arm fully retracted in its travel cradle. It explicitly excludes a platform, ramp, pad, structures, astronauts, extra wheels, and an extended arm.
- **Settings:** Wan2.1 VACE 1.3B, 640×480, 81 frames at 16 fps—5.06 seconds. The 1.3B CausVid LoRA is active for the 8 GB RTX 5060.
- **Output:** MP4 file from `SaveVideo`, under `ComfyUI/output/video/ComfyUI/`.

## Required model files

### Qwen Image 2.1

- `models/diffusion_models/qwen_image_2.1_int8_convrot.safetensors`
- `models/text_encoders/qwen3vl_8b_w4a8.safetensors`
- `models/vae/qwen_image_2.1_vae_bf16.safetensors`

### Wan 2.1 VACE (new workflow)

- `models/diffusion_models/wan2.1_vace_1.3B_fp16.safetensors`
- `models/text_encoders/umt5_xxl_fp8_e4m3fn_scaled.safetensors`
- `models/vae/wan_2.1_vae.safetensors`
- `models/loras/Wan21_CausVid_bidirect2_T2V_1_3B_lora_rank32.safetensors`

The workflows expect ComfyUI 0.37.0 or newer.
