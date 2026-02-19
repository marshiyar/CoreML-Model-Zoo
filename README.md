# CoreML-Model-Zoo

A collection of Core ML (`.mlpackage`) models for image super-resolution, denoising, colorization, and anime-to-sketch conversion. Add any model folder to your Xcode project and use it with the Core ML framework.

Core ML is Apple’s machine learning framework. You can use these models in iOS, iPadOS, macOS, and visionOS apps.

---

## Contents

- [How to use](#how-to-use)
- [Section links](#section-links)
- [Variant naming and compatibility](#variant-naming-and-compatibility)
- [Super Resolution (Real-ESRGAN)](#super-resolution-real-esrgan)
- [Image Denoising (NAFNet)](#image-denoising-nafnet)
- [Image Colorization (DDColor)](#image-colorization-ddcolor)
- [Image2Image (Anime2Sketch)](#image2image-anime2sketch)

---

## How to use

1. Clone or download this repository.
2. Open your Xcode project and add the `.mlpackage` you need:
  - Drag the model folder (for example `Models-List/RealESRGAN_x4/RealESRGAN_x4.mlpackage`) into your app target, or
  - Copy the `.mlpackage` into your project and add it to the target.

Each model’s license follows the original project (see links below). Check the respective repos for terms.

---

## Section links

- **[Super Resolution (Real-ESRGAN)](#super-resolution-real-esrgan)**
  - [RealESRGAN x2](#realesrgan-x2)
  - [RealESRGAN x4](#realesrgan-x4)
- **[Image Denoising (NAFNet)](#image-denoising-nafnet)**
- **[Image Colorization (DDColor)](#image-colorization-ddcolor)**
- **[Image2Image (Anime2Sketch)](#image2image-anime2sketch)**

---

## Variant naming and compatibility

This section reflects the current model filenames in `Models-List/*/*.mlpackage` and the scripts in `Models-List/Scripts/`.


| Pattern / suffix | Meaning |
| ---------------- | ------- |
| `_quant8` | 8-bit linear quantization |
| `_quant4` | 4-bit linear quantization |
| `_palN_kmeans` | N-bit k-means palette/LUT compression |
| `_palN_uniform` | N-bit uniform palette/LUT compression |
| `_linear4` | Linear 4-bit compression variant |
| `_pruned` | Pruned weights variant |
| `_slim`, `_slimmer` | Architecture/compute-reduced variants |
| `_flex1280` | Flexible input variant with upper bound 1280 |
| `_fp16` | FP16-weight variant |
| `_archsame` | Quantized/compressed variant preserving base architecture |
| `_hybrid_q4lut4_50` | Hybrid compression variant |
| `_ios18_...` | iOS 18+ targeted package variant |
| `_xcode` | Xcode-converted/exported variant naming used in this repo |


Compatibility notes:

- `Models-List/Scripts/compare_models.py` expects single-input/single-output models and supports both `multiArrayType` and `imageType`.
- `RealESRGAN_x2plus_flex1280` is the dynamic-shape x2 package in the current repo.
- Variants with `_ios18_` are iOS 18+ packages.
- Local spec-version mapping used in this README: `spec4 -> iOS13+`, `spec6 -> iOS15+`, `spec7 -> iOS16+`, `spec9 -> iOS18+`.

---

## Super Resolution (Real-ESRGAN)

Real-world image super-resolution. Original project: [xinntao/Real-ESRGAN](https://github.com/xinntao/Real-ESRGAN) (BSD-3-Clause).

Models live in `Models-List/RealESRGAN_x2/` and `Models-List/RealESRGAN_x4/`.

### RealESRGAN x2

I/O contract summary:

- Fixed variants use `1x3x256x256 -> 1x3x512x512`.
- In practice, arbitrary input image dimensions are supported in app/runtime flows via tiling/resizing.
- Flex model supports `1x3x[64..1280]^2` natively with dynamic 2x output.
- Deployment target in this folder: `iOS16+`


| Model | Size | Input | Output | Notes |
| --------------------------------------------- | ------- | ----- | ------ | ------------------------ |
| <code>RealESRGAN_<wbr>x2plus.<wbr>mlpackage</code> | 32.5 MB | <img src="https://github.com/marshiyar/CoreML-Model-Zoo/blob/main/Models-List/RealESRGAN_x2/RealESRGAN_x2_model_outputs/input_images/RealESRGAN_x2_model_Input1.png?raw=true" width="120" /> | <img src="https://github.com/marshiyar/CoreML-Model-Zoo/blob/main/Models-List/RealESRGAN_x2/RealESRGAN_x2_model_outputs/output_images/output_images1/RealESRGAN_x2plus.png?raw=true" width="120" /> | Base 2x upscale |
| <code>RealESRGAN_<wbr>x2plus_<wbr>flex1280.<wbr>mlpackage</code> | 32.5 MB |  | <img src="https://github.com/marshiyar/CoreML-Model-Zoo/blob/main/Models-List/RealESRGAN_x2/RealESRGAN_x2_model_outputs/output_images/output_images1/RealESRGAN_x2plus_flex1280.png?raw=true" width="120" /> | Flex, max side 1280 |
| <code>RealESRGAN_<wbr>x2plus_<wbr>quant8.<wbr>mlpackage</code> | 16.8 MB |  | <img src="https://github.com/marshiyar/CoreML-Model-Zoo/blob/main/Models-List/RealESRGAN_x2/RealESRGAN_x2_model_outputs/output_images/output_images1/RealESRGAN_x2plus_quant8.png?raw=true" width="120" /> | INT8 quantized |
| <code>RealESRGAN_<wbr>x2plus_<wbr>pal4.<wbr>mlpackage</code> | 8.7 MB |  | <img src="https://github.com/marshiyar/CoreML-Model-Zoo/blob/main/Models-List/RealESRGAN_x2/RealESRGAN_x2_model_outputs/output_images/output_images1/RealESRGAN_x2plus_pal4.png?raw=true" width="120" /> | Palette 4-bit |
| <code>RealESRGAN_<wbr>x2plus_<wbr>pal6.<wbr>mlpackage</code> | 12.7 MB |  | <img src="https://github.com/marshiyar/CoreML-Model-Zoo/blob/main/Models-List/RealESRGAN_x2/RealESRGAN_x2_model_outputs/output_images/output_images1/RealESRGAN_x2plus_pal6.png?raw=true" width="120" /> | Palette 6-bit |
| <code>RealESRGAN_<wbr>x2plus_<wbr>pal8.<wbr>mlpackage</code> | 16.9 MB |  | <img src="https://github.com/marshiyar/CoreML-Model-Zoo/blob/main/Models-List/RealESRGAN_x2/RealESRGAN_x2_model_outputs/output_images/output_images1/RealESRGAN_x2plus_pal8.png?raw=true" width="120" /> | Palette 8-bit |


### RealESRGAN x4

I/O contract summary:

- Models in this folder use `1x3x256x256 -> 1x3x1024x1024`
- Base package is `iOS15+` (`spec6`); compressed/slim variants are `iOS16+` (`spec7`)


| Model | Size | Input | Output | Notes |
| ------------------------------------------------- | ------- | ----- | ------ | ---------------------------------- |
| <code>RealESRGAN_<wbr>x4.<wbr>mlpackage</code> | 32.5 MB | <img src="https://github.com/marshiyar/CoreML-Model-Zoo/blob/main/Models-List/RealESRGAN_x4/RealESRGAN_x4_model_outputs/input_images/RealESRGAN_x4_model_Input1.png?raw=true" width="120" /> | <img src="https://github.com/marshiyar/CoreML-Model-Zoo/blob/main/Models-List/RealESRGAN_x4/RealESRGAN_x4_model_outputs/output_images/output_images1/RealESRGAN_x4.png?raw=true" width="120" /> | Base 4x upscale |
| <code>RealESRGAN_<wbr>x4_<wbr>slim.<wbr>mlpackage</code> | 16.8 MB |  | <img src="https://github.com/marshiyar/CoreML-Model-Zoo/blob/main/Models-List/RealESRGAN_x4/RealESRGAN_x4_model_outputs/output_images/output_images1/RealESRGAN_x4_slim.png?raw=true" width="120" /> | Slim architecture |
| <code>RealESRGAN_<wbr>x4_<wbr>slimmer.<wbr>mlpackage</code> | 8.8 MB |  | <img src="https://github.com/marshiyar/CoreML-Model-Zoo/blob/main/Models-List/RealESRGAN_x4/RealESRGAN_x4_model_outputs/output_images/output_images1/RealESRGAN_x4_slimmer.png?raw=true" width="120" /> | Slimmer architecture |
| <code>RealESRGAN_<wbr>x4_<wbr>pruned.<wbr>mlpackage</code> | 32.5 MB |  | <img src="https://github.com/marshiyar/CoreML-Model-Zoo/blob/main/Models-List/RealESRGAN_x4/RealESRGAN_x4_model_outputs/output_images/output_images1/RealESRGAN_x4_pruned.png?raw=true" width="120" /> | Pruned |
| <code>RealESRGAN_<wbr>x4_<wbr>quant8.<wbr>mlpackage</code> | 16.8 MB |  | <img src="https://github.com/marshiyar/CoreML-Model-Zoo/blob/main/Models-List/RealESRGAN_x4/RealESRGAN_x4_model_outputs/output_images/output_images1/RealESRGAN_x4_quant8.png?raw=true" width="120" /> | INT8 quantized |
| <code>RealESRGAN_<wbr>x4_<wbr>pal4.<wbr>mlpackage</code> | 8.8 MB |  | <img src="https://github.com/marshiyar/CoreML-Model-Zoo/blob/main/Models-List/RealESRGAN_x4/RealESRGAN_x4_model_outputs/output_images/output_images1/RealESRGAN_x4_pal4.png?raw=true" width="120" /> | Palette 4-bit |


---

## Image Denoising (NAFNet)

Image denoising with NAFNet (SIDD-trained, width 64). Original: [megvii-research/NAFNet](https://github.com/megvii-research/NAFNet).

Models live in `Models-List/NAFNet_SIDD_width64/`.

I/O contract summary:

- `1x3x512x512 -> 1x3x512x512`
- Type: `mlProgram`


| Variant | Size | Input | Output | Notes |
| ------------------------------------------------------ | -------- | ----- | ------ | ------------------------------ |
| <code>NAFNet_<wbr>SIDD_<wbr>width64_<wbr>512.<wbr>mlpackage</code> | 221.7 MB | <img src="https://github.com/marshiyar/CoreML-Model-Zoo/blob/main/Models-List/NAFNet_SIDD_width64/NAFNet_SIDD_width64_model_outputs/input_images/NAFNet_SIDD_width64_model_Input1.png?raw=true" width="120" /> | <img src="https://github.com/marshiyar/CoreML-Model-Zoo/blob/main/Models-List/NAFNet_SIDD_width64/NAFNet_SIDD_width64_model_outputs/output_images/output_images1/NAFNet_SIDD_width64_512.png?raw=true" width="120" /> | Base |
| <code>NAFNet_<wbr>SIDD_<wbr>width64_<wbr>512_<wbr>quant8.<wbr>mlpackage</code> | 111.8 MB |  | <img src="https://github.com/marshiyar/CoreML-Model-Zoo/blob/main/Models-List/NAFNet_SIDD_width64/NAFNet_SIDD_width64_model_outputs/output_images/output_images1/NAFNet_SIDD_width64_512_quant8.png?raw=true" width="120" /> | INT8 |
| <code>NAFNet_<wbr>SIDD_<wbr>width64_<wbr>512_<wbr>ios18_<wbr>quant4.<wbr>mlpackage</code> | 56.7 MB |  | <img src="https://github.com/marshiyar/CoreML-Model-Zoo/blob/main/Models-List/NAFNet_SIDD_width64/NAFNet_SIDD_width64_model_outputs/output_images/output_images1/NAFNet_SIDD_width64_512_ios18_quant4.png?raw=true" width="120" /> | iOS18, 4-bit quant |
| <code>NAFNet_<wbr>SIDD_<wbr>width64_<wbr>512_<wbr>pal6_<wbr>kmeans.<wbr>mlpackage</code> | 83.9 MB |  | <img src="https://github.com/marshiyar/CoreML-Model-Zoo/blob/main/Models-List/NAFNet_SIDD_width64/NAFNet_SIDD_width64_model_outputs/output_images/output_images1/NAFNet_SIDD_width64_512_pal6_kmeans.png?raw=true" width="120" /> | 6-bit palette (kmeans) |
| <code>NAFNet_<wbr>SIDD_<wbr>width64_<wbr>512_<wbr>pal8_<wbr>kmeans.<wbr>mlpackage</code> | 111.6 MB |  | <img src="https://github.com/marshiyar/CoreML-Model-Zoo/blob/main/Models-List/NAFNet_SIDD_width64/NAFNet_SIDD_width64_model_outputs/output_images/output_images1/NAFNet_SIDD_width64_512_pal8_kmeans.png?raw=true" width="120" /> | 8-bit palette (kmeans) |
| <code>NAFNet_<wbr>SIDD_<wbr>width64_<wbr>512_<wbr>pal8_<wbr>uniform.<wbr>mlpackage</code> | 111.6 MB |  | <img src="https://github.com/marshiyar/CoreML-Model-Zoo/blob/main/Models-List/NAFNet_SIDD_width64/NAFNet_SIDD_width64_model_outputs/output_images/output_images1/NAFNet_SIDD_width64_512_pal8_uniform.png?raw=true" width="120" /> | 8-bit palette (uniform) |


---

## Image Colorization (DDColor)

Grayscale image colorization. ModelScope variant. Original: [piddnad/DDColor](https://github.com/piddnad/DDColor).

Models live in `Models-List/DDColor/`.

I/O contract summary:

- `gray_rgb:1x3x512x512 -> ab:1x2x512x512`
- Type: `mlProgram`


| Variant | Size | Input | Output | Notes |
| ----------------------------------------------------- | -------- | ----- | ------ | ------------------------------ |
| <code>DDColor_<wbr>modelscope_<wbr>512.<wbr>mlpackage</code> | 445.5 MB | <img src="https://github.com/marshiyar/CoreML-Model-Zoo/blob/main/Models-List/DDColor/DDColor_Model_outputs/input_images/DDColor_model_Input1.png?raw=true" width="120" /> | <img src="https://github.com/marshiyar/CoreML-Model-Zoo/blob/main/Models-List/DDColor/DDColor_Model_outputs/output_images/output_images1/DDColor_modelscope_512.png?raw=true" width="120" /> | Base |
| <code>DDColor_<wbr>modelscope_<wbr>512_<wbr>quant8.<wbr>mlpackage</code> | 223.8 MB |  | <img src="https://github.com/marshiyar/CoreML-Model-Zoo/blob/main/Models-List/DDColor/DDColor_Model_outputs/output_images/output_images1/DDColor_modelscope_512_quant8.png?raw=true" width="120" /> | INT8 |
| <code>DDColor_<wbr>modelscope_<wbr>512_<wbr>ios18_<wbr>quant4.<wbr>mlpackage</code> | 112.7 MB |  | <img src="https://github.com/marshiyar/CoreML-Model-Zoo/blob/main/Models-List/DDColor/DDColor_Model_outputs/output_images/output_images1/DDColor_modelscope_512_ios18_quant4.png?raw=true" width="120" /> | iOS18, 4-bit quant |
| <code>DDColor_<wbr>modelscope_<wbr>512_<wbr>ios18_<wbr>pal3_<wbr>kmeans.<wbr>mlpackage</code> | 84.4 MB |  | <img src="https://github.com/marshiyar/CoreML-Model-Zoo/blob/main/Models-List/DDColor/DDColor_Model_outputs/output_images/output_images1/DDColor_modelscope_512_ios18_pal3_kmeans.png?raw=true" width="120" /> | iOS18, 3-bit palette (kmeans) |
| <code>DDColor_<wbr>modelscope_<wbr>512_<wbr>pal4_<wbr>kmeans.<wbr>mlpackage</code> | 112.2 MB |  | <img src="https://github.com/marshiyar/CoreML-Model-Zoo/blob/main/Models-List/DDColor/DDColor_Model_outputs/output_images/output_images1/DDColor_modelscope_512_pal4_kmeans.png?raw=true" width="120" /> | 4-bit palette (kmeans) |
| <code>DDColor_<wbr>modelscope_<wbr>512_<wbr>pal6_<wbr>kmeans.<wbr>mlpackage</code> | 167.8 MB |  | <img src="https://github.com/marshiyar/CoreML-Model-Zoo/blob/main/Models-List/DDColor/DDColor_Model_outputs/output_images/output_images1/DDColor_modelscope_512_pal6_kmeans.png?raw=true" width="120" /> | 6-bit palette (kmeans) |
| <code>DDColor_<wbr>modelscope_<wbr>512_<wbr>pal6_<wbr>uniform.<wbr>mlpackage</code> | 167.8 MB |  | <img src="https://github.com/marshiyar/CoreML-Model-Zoo/blob/main/Models-List/DDColor/DDColor_Model_outputs/output_images/output_images1/DDColor_modelscope_512_pal6_uniform.png?raw=true" width="120" /> | 6-bit palette (uniform) |
| <code>DDColor_<wbr>modelscope_<wbr>512_<wbr>pal8_<wbr>kmeans.<wbr>mlpackage</code> | 223.4 MB |  | <img src="https://github.com/marshiyar/CoreML-Model-Zoo/blob/main/Models-List/DDColor/DDColor_Model_outputs/output_images/output_images1/DDColor_modelscope_512_pal8_kmeans.png?raw=true" width="120" /> | 8-bit palette (kmeans) |
| <code>DDColor_<wbr>modelscope_<wbr>512_<wbr>pal8_<wbr>uniform.<wbr>mlpackage</code> | 223.4 MB |  | <img src="https://github.com/marshiyar/CoreML-Model-Zoo/blob/main/Models-List/DDColor/DDColor_Model_outputs/output_images/output_images1/DDColor_modelscope_512_pal8_uniform.png?raw=true" width="120" /> | 8-bit palette (uniform) |


---

## Image2Image (Anime2Sketch)

Anime/style artwork to sketch conversion. Original: [Mukosame/Anime2Sketch](https://github.com/Mukosame/Anime2Sketch) (MIT).

Models live in `Models-List/anime2sketch/`.

I/O contract summary:

- Main neural-network variants: `512x512 -> 512x512` (`spec4`, iOS13+)
- Ensemble overlay variants: pipeline `512x512 -> 1024x1024` (`spec7`, iOS16+)


| Model | Size | Input | Output | Notes |
| ------------------------------------------------------------- | -------- | ----- | ------ | --------------------------------- |
| <code>anime2sketch.<wbr>mlpackage</code> | 207.6 MB | <img src="https://github.com/marshiyar/CoreML-Model-Zoo/blob/main/Models-List/anime2sketch/Anime2Sketch_x4_model_outputs/input_images/Anime2Sketch_model_Input1.png?raw=true" width="120" /> | <img src="https://github.com/marshiyar/CoreML-Model-Zoo/blob/main/Models-List/anime2sketch/Anime2Sketch_x4_model_outputs/output_images/output_images1/anime2sketch.png?raw=true" width="120" /> | Base |
| <code>anime2sketch_<wbr>xcode_<wbr>fp16.<wbr>mlpackage</code> | 103.8 MB |  | <img src="https://github.com/marshiyar/CoreML-Model-Zoo/blob/main/Models-List/anime2sketch/Anime2Sketch_x4_model_outputs/output_images/output_images1/anime2sketch_xcode_fp16.png?raw=true" width="120" /> | FP16 |
| <code>anime2sketch_<wbr>xcode_<wbr>quant8.<wbr>mlpackage</code> | 51.9 MB |  | <img src="https://github.com/marshiyar/CoreML-Model-Zoo/blob/main/Models-List/anime2sketch/Anime2Sketch_x4_model_outputs/output_images/output_images1/anime2sketch_xcode_quant8.png?raw=true" width="120" /> | INT8 |
| <code>anime2sketch_<wbr>xcode_<wbr>archsame_<wbr>quant4.<wbr>mlpackage</code> | 26.0 MB |  | <img src="https://github.com/marshiyar/CoreML-Model-Zoo/blob/main/Models-List/anime2sketch/Anime2Sketch_x4_model_outputs/output_images/output_images1/anime2sketch_xcode_archsame_quant4.png?raw=true" width="120" /> | Same arch, 4-bit |
| <code>anime2sketch_<wbr>xcode_<wbr>archsame_<wbr>quant8.<wbr>mlpackage</code> | 51.9 MB |  | <img src="https://github.com/marshiyar/CoreML-Model-Zoo/blob/main/Models-List/anime2sketch/Anime2Sketch_x4_model_outputs/output_images/output_images1/anime2sketch_xcode_archsame_quant8.png?raw=true" width="120" /> | Same arch, 8-bit |
| <code>anime2sketch_<wbr>xcode_<wbr>archsame_<wbr>pal4.<wbr>mlpackage</code> | 26.0 MB |  | <img src="https://github.com/marshiyar/CoreML-Model-Zoo/blob/main/Models-List/anime2sketch/Anime2Sketch_x4_model_outputs/output_images/output_images1/anime2sketch_xcode_archsame_pal4.png?raw=true" width="120" /> | Same arch, pal4 |
| <code>anime2sketch_<wbr>xcode_<wbr>lut4.<wbr>mlpackage</code> | 26.0 MB |  | <img src="https://github.com/marshiyar/CoreML-Model-Zoo/blob/main/Models-List/anime2sketch/Anime2Sketch_x4_model_outputs/output_images/output_images1/anime2sketch_xcode_lut4.png?raw=true" width="120" /> | LUT 4-bit |
| <code>anime2sketch_<wbr>xcode_<wbr>lut6.<wbr>mlpackage</code> | 38.9 MB |  | <img src="https://github.com/marshiyar/CoreML-Model-Zoo/blob/main/Models-List/anime2sketch/Anime2Sketch_x4_model_outputs/output_images/output_images1/anime2sketch_xcode_lut6.png?raw=true" width="120" /> | LUT 6-bit |
| <code>anime2sketch_<wbr>xcode_<wbr>linear4.<wbr>mlpackage</code> | 26.0 MB |  | <img src="https://github.com/marshiyar/CoreML-Model-Zoo/blob/main/Models-List/anime2sketch/Anime2Sketch_x4_model_outputs/output_images/output_images1/anime2sketch_xcode_linear4.png?raw=true" width="120" /> | Linear 4-bit |
| <code>anime2sketch_<wbr>xcode_<wbr>hybrid_<wbr>q4lut4_<wbr>50.<wbr>mlpackage</code> | 26.0 MB |  | <img src="https://github.com/marshiyar/CoreML-Model-Zoo/blob/main/Models-List/anime2sketch/Anime2Sketch_x4_model_outputs/output_images/output_images1/anime2sketch_xcode_hybrid_q4lut4_50.png?raw=true" width="120" /> | Hybrid quant |


---

## Thanks

Thanks to the authors of Real-ESRGAN, NAFNet, DDColor, and Anime2Sketch for the original models and code.

---

## Author

[Your Name]  
[Your Title / Role]  
Contact: [your@email.com](mailto:your@email.com)  
[GitHub](https://github.com/[your-username])
