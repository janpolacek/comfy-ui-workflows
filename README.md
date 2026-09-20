# ComfyUI Workflows

Curated local ComfyUI workflows for the fictional Red Horizon Mars exploration programme.
The prompts and visual direction are based on [mars-ai-simulation.janpolacek.workers.dev](https://mars-ai-simulation.janpolacek.workers.dev), specifically the published mission records cited below. The still and video prompts request photorealistic mission visualizations; the underlying project remains fictional.

## Repository layout

- `workflows/` contains loadable ComfyUI workflow JSON files.
- `assets/inputs/pathfinder/` contains the copied RH-01 Pathfinder reference images used by the edit and video workflows.
- `assets/outputs/final-approach/` contains generated Qwen final-approach stills.
- `assets/outputs/pathfinder/` contains Pathfinder still renders and `assets/outputs/pathfinder/video/` contains VACE video renders.

Every input and output archived here is intentionally versioned in Git.

## Workflows

### Qwen Image 2.1 — Text to Image

`workflows/Qwen-Image-2.1-Text-to-Image.json`

- **Purpose:** Generate the final approach correction artwork.
- **Prompt source:** `website/news/006-cruise-final-approach.mdx`.
- **Prompt:** A photorealistic, precise uncrewed course-refinement manoeuvre in interplanetary cruise, with Mars ahead, hard solar light, credible spacecraft materials, and no people, logos, flags, or text.
- **Inputs:** Text prompt, seed, resolution, and the installed Qwen Image 2.1 weights.
- **Archived output:** [`assets/outputs/final-approach/rh01-final-approach-qwen-2.1.png`](assets/outputs/final-approach/rh01-final-approach-qwen-2.1.png), 1024×1024 PNG.

### Qwen Image 2.1 — Image Edit

`workflows/Qwen-Image-2.1-Image-Edit.json`

- **Purpose:** Render RH-01 Pathfinder on a measured traverse through wild, unprepared Mars terrain.
- **Prompt sources:** `website/news/008-landing.mdx`, `website/news/009-egress.mdx`, and `docs/vehicles/pathfinder/VEHICLE.md`.
- **Inputs:** Pathfinder reference images already selected in the local workflow: `canonical.png`, `front-left.png`, `rear-right.png`, and `contact-arm.png`.
- **Prompt:** A photorealistic rover on rough, brute, natural Martian regolith with loose gravel, rocks, and natural ridges. The contact arm remains retracted; six open-mesh wheels leave restrained fresh tracks. It excludes prepared surfaces, platforms, pads, ramps, structures, and spacecraft hardware.
- **Archived outputs:** `assets/outputs/pathfinder/01-egress_00001_.png` through `01-egress_00004_.png` are previous Pathfinder scene renders. Future image-edit results belong in this same folder.

### Wan 2.1 VACE — Pathfinder Multi-Reference Video

`workflows/Wan2.1-VACE-Pathfinder-Multi-Reference-Video.json`

- **Purpose:** Generate a short reference-guided video of a dust-covered RH-01 Pathfinder driving across Asteria Field.
- **Prompt sources:** `website/news/010-health-review.mdx` and `docs/vehicles/pathfinder/VEHICLE.md`.
- **Inputs:** Five Pathfinder views—`canonical.png`, `front-left.png`, `rear-right.png`, `side-view.png`, and `contact-arm.png`—are stitched into a single reference board before reaching `WanVaceToVideo`. The native VACE node accepts one reference-image input, so the board preserves multiple useful viewpoints in that one input.
- **Prompt:** Photorealistic scientific rover footage on rough, wild, unprepared Martian regolith. The six wheels continuously rotate and compress soil, the suspension responds to rocks, and two clean parallel tracks form behind the rover. The contact arm stays fully retracted. The negative prompt excludes cartoon/illustration/CGI styling, static wheels, missing tracks, platforms, pads, ramps, structures, and people.
- **Settings:** Wan2.1 VACE 1.3B, 640×480, 61 frames at 12 fps—5.08 seconds. The CausVid LoRA is bypassed and the workflow uses 20 steps / CFG 6 for a higher-quality, slower render on the 8 GB RTX 5060.
- **Output:** MP4 file from `SaveVideo`, under `ComfyUI/output/video/`. The improved render is archived at [`assets/outputs/pathfinder/video/pathfinder-vace-asteria-field-quality.mp4`](assets/outputs/pathfinder/video/pathfinder-vace-asteria-field-quality.mp4).

## Required model files

### Qwen Image 2.1

- `models/diffusion_models/qwen_image_2.1_int8_convrot.safetensors`
- `models/text_encoders/qwen3vl_8b_int8_convrot.safetensors`
- `models/vae/qwen_image_2.1_vae_bf16.safetensors`

### Wan 2.1 VACE (new workflow)

- `models/diffusion_models/wan2.1_vace_1.3B_fp16.safetensors`
- `models/text_encoders/umt5_xxl_fp8_e4m3fn_scaled.safetensors`
- `models/vae/wan_2.1_vae.safetensors`
- `models/loras/Wan21_CausVid_bidirect2_T2V_1_3B_lora_rank32.safetensors` (installed but bypassed in the quality workflow)

The workflows expect ComfyUI 0.37.0 or newer.
