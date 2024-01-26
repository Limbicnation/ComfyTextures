# Comfy Textures

Comfy Textures is an Unreal Engine plugin which integrates the editor with [ComfyUI](https://github.com/comfyanonymous/ComfyUI).
It allows you to quickly create and refine textures for your scene using generative diffusion models.

Features:

- [x] Single point-of-view texture projection
- [ ] Multiple point-of-view texture projection (WIP)
- [x] Perspective camera
- [x] Orthographic camera
- [x] Inpainting
- [x] Image to image
- [x] Remote ComfyUI instance support

Unreal Engine 5.x is supported. Should work with 4.x with minor code changes.

## Watch the demo

https://github.com/AlexanderDzhoganov/ComfyTextures/assets/855464/6a674673-bbe4-42d1-a12b-f43edfc87640

## Comfy Textures Editor Widget

<img src='.ghassets/widget.png' width='300'>

## Support & Contributing

Join the [Discord](https://discord.gg/qpS7RMKGVj) for help and support.

If you want to contribute to the project, feel free to open a pull request or an issue.

# Installation

### Setup ComfyUI

1. Install [ComfyUI](https://github.com/comfyanonymous/ComfyUI) by following the [official installation instructions](https://github.com/comfyanonymous/ComfyUI?tab=readme-ov-file#installing) for your OS.

2. Download the necessary models and place them in the ComfyUI `models` directory.

The models directory is relative to the ComfyUI root directory i.e. `<ComfyUI Root>/ComfyUI/models/`.

- `models/checkpoints/sd_xl_base_1.0_0.9vae.safetensors` - [Download](https://huggingface.co/stabilityai/stable-diffusion-xl-base-1.0/blob/main/sd_xl_base_1.0_0.9vae.safetensors)
- `models/checkpoints/sd_xl_refiner_1.0_0.9vae.safetensors` - [Download](https://huggingface.co/stabilityai/stable-diffusion-xl-refiner-1.0/blob/main/sd_xl_refiner_1.0_0.9vae.safetensors)
- `models/controlnet/control-lora-canny-rank256.safetensors` - [Download](https://huggingface.co/stabilityai/control-lora/blob/main/control-LoRAs-rank256/control-lora-canny-rank256.safetensors)
- `models/controlnet/control-lora-depth-rank256.safetensors` - [Download](https://huggingface.co/stabilityai/control-lora/blob/main/control-LoRAs-rank256/control-lora-depth-rank256.safetensors)
- `models/loras/lcm_lora_sdxl.safetensors` - [Download](https://huggingface.co/latent-consistency/lcm-lora-sdxl/blob/main/pytorch_lora_weights.safetensors) (Note: Rename the file to `lcm_lora_sdxl.safetensors`)
- `models/upscale_models/4x-UltraSharp.pth` - [Download](https://huggingface.co/lokCX/4x-Ultrasharp/blob/main/4x-UltraSharp.pth)

### Setup Unreal Engine project

1. Clone this repository and open the project (`MyProject.uproject`) in the Unreal Engine editor.

2. Configure the plugin by going to `Project Settings -> Plugins -> Comfy Textures`.

If you are running ComfyUI on a remote machine, you need to set the `Comfy Url` to the correct address.

3. Open the plugin window by clicking on `Tools -> Editor Utility Widgets -> Comfy Textures Widget`.

Note: If the menu item is missing you need to open the `ComfyTexturesWidget` from the content browser in `Plugins/Comfy Textures Content/` and click `Run Utility Widget` in the blueprint editor.

# Usage

Note: Make sure ComfyUI is up and running before proceeding.

1. Select the actors you want to texture in the Outliner.

2. Set your desired settings in the Comfy Textures widget.

3. Click `Render` to start the rendering process.

Notes:
- Make sure your meshes have UVs (autogenerated UVs are fine).
- The plugin will automatically create a new material instance and texture for each selected actor.

## Modes

### Create

This mode uses a fast SDXL LCM model to create a low-resolution texture for each selected actor. Use this to quickly prototype and iterate on your scene.

### Refine

This mode uses a slower SDXL workflow to refine the low-resolution textures created in the `Create` mode. Use this to create the final high-resolution textures for your scene.

### Edit

This mode allows you to edit the textures created in the `Create` or `Refine` mode by using an inpainting workflow. Use this mode to fix any artifacts or errors in the textures.

You can select from two edit modes - `From Texture` and `From Object`. `From Texture` allows you to do precise edits by painting undesired areas to magenta (255, 0, 255, 255) using Mesh Paint. `From Object` will inpaint all selected actors.

## Editing the ComfyUI Workflows

You can find the ComfyUI workflows used by the plugin in the `Plugins/ComfyTextures/Content/Workflows/Original` folder. Load the JSONs into ComfyUI to see the full workflow and make changes. After making changes, save the workflow using the `Save (API Format)` button in ComfyUI and copy the JSON to the corresponding file in the `Plugins/ComfyTextures/Content/Workflows` folder.

Note: You need to have `Enable Dev mode Options` enabled in the ComfyUI settings to see the `Save (API Format)` button.

# Credits

Made by me (Alexander Dzhoganov). If you are hiring, hit me up at alexanderdzhoganov [at] gmail [dot] com.

Thank you to the Stability.ai and to the ComfyUI teams for their wonderful work Stable Diffusion and ComfyUI.