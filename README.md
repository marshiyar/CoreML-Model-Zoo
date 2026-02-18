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
3. Use the generated Swift API or `MLModel` / `VNCoreMLRequest` in your code.

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

This section is based on `Models-List/Scripts` (`compress_model.py`, `slim_architecture.py`, `convert_realesrgan_x2plus_to_coreml.py`, `compare_models.py`) and local model specs in this repo.


| Pattern / suffix             | Meaning                                                     |
| ---------------------------- | ----------------------------------------------------------- |
| `_quant8`                    | 8-bit linear quantization                                   |
| `_quant4`                    | 4-bit linear quantization                                   |
| `_palN_kmeans`               | N-bit k-means palettization (LUT)                           |
| `_palN_uniform` / `_linearN` | N-bit uniform/linear LUT palettization                      |
| `_pal_unique`                | Unique-value palette variant                                |
| `_pruned`                    | Threshold pruning (mlProgram path in scripts)               |
| `_slim`, `_slimmer`          | Architecture/compute-reduced variants                       |
| `arch_b*_nf*_gc`*            | RRDB architecture-slim variants from `slim_architecture.py` |
| `_flex`, `_flex1280`         | Flexible input size variants (RangeDim bounds)              |
| `_hybrid_q4lut4_50`          | Hybrid neural-network compression (mixed LUT4 + linear4)    |
| `_wrapped`                   | Wrapped/pipeline style package                              |


Compatibility notes:

- `compare_models.py` expects single-input/single-output models and supports both `multiArrayType` and `imageType`.
- `convert_realesrgan_x2plus_to_coreml.py` enforces even input height/width for x2plus conversion; flex variants keep that rule.
- 4-bit mlProgram variants in this repo are in iOS 18+ spec packages.
- Local spec version mapping used in tables: `spec4 -> iOS13+`, `spec6 -> iOS15+`, `spec7 -> iOS16+`, `spec9 -> iOS18+`.

---

## Super Resolution (Real-ESRGAN)

Real-world image super-resolution. Original project: [xinntao/Real-ESRGAN](https://github.com/xinntao/Real-ESRGAN) (BSD-3-Clause).

Models live in `Models-List/RealESRGAN_x2/` and `Models-List/RealESRGAN_x4/`.

### RealESRGAN x2

I/O contract summary:

- Fixed models: `1x3x256x256 -> 1x3x512x512`
- Flex models: `1x3x[64..1024]^2` or `1x3x[64..1280]^2` with dynamic 2x output
- Deployment target in this folder: `iOS16+`


| Model                                         | Type        | Min target | I/O                              | Size    | Input | Output | Notes                    |
| --------------------------------------------- | ----------- | ---------- | -------------------------------- | ------- | ----- | ------ | ------------------------ |
| `RealESRGAN_x2plus.mlpackage`                 | `mlProgram` | iOS16+     | `1x3x256x256 -> 1x3x512x512`     | 32.5 MB |       |        | Base 2x upscale          |
| `RealESRGAN_x2plus_flex.mlpackage`            | `mlProgram` | iOS16+     | `1x3x[64..1024]^2 -> dynamic 2x` | 32.5 MB |       |        | Flexible input size      |
| `RealESRGAN_x2plus_flex1280.mlpackage`        | `mlProgram` | iOS16+     | `1x3x[64..1280]^2 -> dynamic 2x` | 32.5 MB |       |        | Flex, max side 1280      |
| `RealESRGAN_x2plus_pruned.mlpackage`          | `mlProgram` | iOS16+     | `1x3x256x256 -> 1x3x512x512`     | 32.5 MB |       |        | Pruned                   |
| `RealESRGAN_x2plus_quant8.mlpackage`          | `mlProgram` | iOS16+     | `1x3x256x256 -> 1x3x512x512`     | 16.8 MB |       |        | INT8 quantized           |
| `RealESRGAN_x2plus_pal4.mlpackage`            | `mlProgram` | iOS16+     | `1x3x256x256 -> 1x3x512x512`     | 8.7 MB  |       |        | Palette 4-bit            |
| `RealESRGAN_x2plus_pal6.mlpackage`            | `mlProgram` | iOS16+     | `1x3x256x256 -> 1x3x512x512`     | 12.7 MB |       |        | Palette 6-bit            |
| `RealESRGAN_x2plus_pal8.mlpackage`            | `mlProgram` | iOS16+     | `1x3x256x256 -> 1x3x512x512`     | 16.9 MB |       |        | Palette 8-bit            |
| `RealESRGAN_x2plus_flex1280_pruned.mlpackage` | `mlProgram` | iOS16+     | `1x3x[64..1280]^2 -> dynamic 2x` | 32.5 MB |       |        | Flex1280 + pruned        |
| `RealESRGAN_x2plus_flex1280_quant8.mlpackage` | `mlProgram` | iOS16+     | `1x3x[64..1280]^2 -> dynamic 2x` | 16.8 MB |       |        | Flex1280 + INT8          |
| `RealESRGAN_x2plus_flex1280_pal4.mlpackage`   | `mlProgram` | iOS16+     | `1x3x[64..1280]^2 -> dynamic 2x` | 8.7 MB  |       |        | Flex1280 + palette 4-bit |
| `RealESRGAN_x2plus_flex1280_pal6.mlpackage`   | `mlProgram` | iOS16+     | `1x3x[64..1280]^2 -> dynamic 2x` | 12.7 MB |       |        | Flex1280 + palette 6-bit |
| `RealESRGAN_x2plus_flex1280_pal8.mlpackage`   | `mlProgram` | iOS16+     | `1x3x[64..1280]^2 -> dynamic 2x` | 16.8 MB |       |        | Flex1280 + palette 8-bit |
| `RealESRGAN_x2_wrapped.mlpackage`             | `pipeline`  | iOS16+     | `1x3x256x256 -> 1x3x512x512`     | 32.5 MB |       |        | Wrapped pipeline variant |


### RealESRGAN x4

I/O contract summary:

- Models in this folder use `1x3x256x256 -> 1x3x1024x1024`
- Base package is `iOS15+` (`spec6`); compressed/slim variants are `iOS16+` (`spec7`)


| Model                                             | Type        | Min target | I/O                            | Size    | Input | Output | Notes                              |
| ------------------------------------------------- | ----------- | ---------- | ------------------------------ | ------- | ----- | ------ | ---------------------------------- |
| `RealESRGAN_x4.mlpackage`                         | `mlProgram` | iOS15+     | `1x3x256x256 -> 1x3x1024x1024` | 32.5 MB | <img src="https://github.com/marshiyar/CoreML-Model-Zoo/blob/main/Models-List/RealESRGAN_x4/RealESRGAN_x4_model_outputs/input_images/RealESRGAN_x4_model_Input1.png?raw=true" width="120" /> | <img src="https://github.com/marshiyar/CoreML-Model-Zoo/blob/main/Models-List/RealESRGAN_x4/RealESRGAN_x4_model_outputs/output_images/output_images1/RealESRGAN_x4.png?raw=true" width="120" /> | Base 4x upscale                    |
| `RealESRGAN_x4_slim.mlpackage`                    | `mlProgram` | iOS16+     | `1x3x256x256 -> 1x3x1024x1024` | 16.8 MB |       | <img src="https://github.com/marshiyar/CoreML-Model-Zoo/blob/main/Models-List/RealESRGAN_x4/RealESRGAN_x4_model_outputs/output_images/output_images1/RealESRGAN_x4_slim.png?raw=true" width="120" /> | Slim architecture                  |
| `RealESRGAN_x4_slimmer.mlpackage`                 | `mlProgram` | iOS16+     | `1x3x256x256 -> 1x3x1024x1024` | 8.8 MB  |       | <img src="https://github.com/marshiyar/CoreML-Model-Zoo/blob/main/Models-List/RealESRGAN_x4/RealESRGAN_x4_model_outputs/output_images/output_images1/RealESRGAN_x4_slimmer.png?raw=true" width="120" /> | Slimmer architecture               |
| `RealESRGAN_x4_pruned.mlpackage`                  | `mlProgram` | iOS16+     | `1x3x256x256 -> 1x3x1024x1024` | 32.5 MB |       | <img src="https://github.com/marshiyar/CoreML-Model-Zoo/blob/main/Models-List/RealESRGAN_x4/RealESRGAN_x4_model_outputs/output_images/output_images1/RealESRGAN_x4_pruned.png?raw=true" width="120" /> | Pruned                             |
| `RealESRGAN_x4_quant8.mlpackage`                  | `mlProgram` | iOS16+     | `1x3x256x256 -> 1x3x1024x1024` | 16.8 MB |       | <img src="https://github.com/marshiyar/CoreML-Model-Zoo/blob/main/Models-List/RealESRGAN_x4/RealESRGAN_x4_model_outputs/output_images/output_images1/RealESRGAN_x4_quant8.png?raw=true" width="120" /> | INT8 quantized                     |
| `RealESRGAN_x4_pal4.mlpackage`                    | `mlProgram` | iOS16+     | `1x3x256x256 -> 1x3x1024x1024` | 8.8 MB  |       | <img src="https://github.com/marshiyar/CoreML-Model-Zoo/blob/main/Models-List/RealESRGAN_x4/RealESRGAN_x4_model_outputs/output_images/output_images1/RealESRGAN_x4_pal4.png?raw=true" width="120" /> | Palette 4-bit                      |
| `RealESRGAN_x4_arch_b8_nf48_gc24_xcode.mlpackage` | `mlProgram` | iOS16+     | `1x3x256x256 -> 1x3x1024x1024` | 6.6 MB  |       | <img src="https://github.com/marshiyar/CoreML-Model-Zoo/blob/main/Models-List/RealESRGAN_x4/RealESRGAN_x4_model_outputs/output_images/output_images1/RealESRGAN_x4_arch_b8_xcode.png?raw=true" width="120" /> | Architecture-slim (`b8,nf48,gc24`) |
| `RealESRGAN_x4_arch_b6_nf40_gc20_xcode.mlpackage` | `mlProgram` | iOS16+     | `1x3x256x256 -> 1x3x1024x1024` | 3.5 MB  |       |        | Architecture-slim (`b6,nf40,gc20`) |
| `RealESRGAN_x4_iphone_fast.mlpackage`             | `mlProgram` | iOS16+     | `1x3x256x256 -> 1x3x1024x1024` | 6.6 MB  |       |        | iPhone-focused fast variant        |
| `RealESRGAN_x4_iphone_fast_quant8.mlpackage`      | `mlProgram` | iOS16+     | `1x3x256x256 -> 1x3x1024x1024` | 3.5 MB  |       |        | iPhone-fast + INT8                 |


---

## Image Denoising (NAFNet)

Image denoising with NAFNet (SIDD-trained, width 64). Original: [megvii-research/NAFNet](https://github.com/megvii-research/NAFNet).

Models live in `Models-List/NAFNet_SIDD_width64/`.

I/O contract summary:

- `1x3x512x512 -> 1x3x512x512`
- Type: `mlProgram`


| Variant                                                | Type        | Min target | I/O                          | Size     | Input | Output | Notes                          |
| ------------------------------------------------------ | ----------- | ---------- | ---------------------------- | -------- | ----- | ------ | ------------------------------ |
| `NAFNet_SIDD_width64_512.mlpackage`                    | `mlProgram` | iOS16+     | `1x3x512x512 -> 1x3x512x512` | 221.7 MB |       |        | Base                           |
| `NAFNet_SIDD_width64_512_quant8.mlpackage`             | `mlProgram` | iOS16+     | `1x3x512x512 -> 1x3x512x512` | 111.8 MB |       |        | INT8                           |
| `NAFNet_SIDD_width64_512_ios18.mlpackage`              | `mlProgram` | iOS18+     | `1x3x512x512 -> 1x3x512x512` | 221.7 MB |       |        | iOS 18 spec                    |
| `NAFNet_SIDD_width64_512_ios18_quant4.mlpackage`       | `mlProgram` | iOS18+     | `1x3x512x512 -> 1x3x512x512` | 56.7 MB  |       |        | iOS18, 4-bit quant             |
| `NAFNet_SIDD_width64_512_ios18_pal3_kmeans.mlpackage`  | `mlProgram` | iOS18+     | `1x3x512x512 -> 1x3x512x512` | 42.5 MB  |       |        | iOS18, 3-bit palette (kmeans)  |
| `NAFNet_SIDD_width64_512_ios18_pal3_uniform.mlpackage` | `mlProgram` | iOS18+     | `1x3x512x512 -> 1x3x512x512` | 42.5 MB  |       |        | iOS18, 3-bit palette (uniform) |
| `NAFNet_SIDD_width64_512_pal1_kmeans.mlpackage`        | `mlProgram` | iOS16+     | `1x3x512x512 -> 1x3x512x512` | 14.9 MB  |       |        | 1-bit palette (kmeans)         |
| `NAFNet_SIDD_width64_512_pal1_uniform.mlpackage`       | `mlProgram` | iOS16+     | `1x3x512x512 -> 1x3x512x512` | 14.9 MB  |       |        | 1-bit palette (uniform)        |
| `NAFNet_SIDD_width64_512_pal2_kmeans.mlpackage`        | `mlProgram` | iOS16+     | `1x3x512x512 -> 1x3x512x512` | 28.7 MB  |       |        | 2-bit palette (kmeans)         |
| `NAFNet_SIDD_width64_512_pal2_uniform.mlpackage`       | `mlProgram` | iOS16+     | `1x3x512x512 -> 1x3x512x512` | 28.7 MB  |       |        | 2-bit palette (uniform)        |
| `NAFNet_SIDD_width64_512_pal4_kmeans.mlpackage`        | `mlProgram` | iOS16+     | `1x3x512x512 -> 1x3x512x512` | 56.3 MB  |       |        | 4-bit palette (kmeans)         |
| `NAFNet_SIDD_width64_512_pal4_uniform.mlpackage`       | `mlProgram` | iOS16+     | `1x3x512x512 -> 1x3x512x512` | 56.3 MB  |       |        | 4-bit palette (uniform)        |
| `NAFNet_SIDD_width64_512_pal6_kmeans.mlpackage`        | `mlProgram` | iOS16+     | `1x3x512x512 -> 1x3x512x512` | 83.9 MB  |       |        | 6-bit palette (kmeans)         |
| `NAFNet_SIDD_width64_512_pal6_uniform.mlpackage`       | `mlProgram` | iOS16+     | `1x3x512x512 -> 1x3x512x512` | 83.9 MB  |       |        | 6-bit palette (uniform)        |
| `NAFNet_SIDD_width64_512_pal8_kmeans.mlpackage`        | `mlProgram` | iOS16+     | `1x3x512x512 -> 1x3x512x512` | 111.6 MB |       |        | 8-bit palette (kmeans)         |
| `NAFNet_SIDD_width64_512_pal8_uniform.mlpackage`       | `mlProgram` | iOS16+     | `1x3x512x512 -> 1x3x512x512` | 111.6 MB |       |        | 8-bit palette (uniform)        |


---

## Image Colorization (DDColor)

Grayscale image colorization. ModelScope variant. Original: [piddnad/DDColor](https://github.com/piddnad/DDColor).

Models live in `Models-List/DDColor/`.

I/O contract summary:

- `gray_rgb:1x3x512x512 -> ab:1x2x512x512`
- Type: `mlProgram`


| Variant                                               | Type        | Min target | I/O                          | Size     | Input | Output | Notes                          |
| ----------------------------------------------------- | ----------- | ---------- | ---------------------------- | -------- | ----- | ------ | ------------------------------ |
| `DDColor_modelscope_512.mlpackage`                    | `mlProgram` | iOS16+     | `1x3x512x512 -> 1x2x512x512` | 445.5 MB |       |        | Base                           |
| `DDColor_modelscope_512_pruned.mlpackage`             | `mlProgram` | iOS16+     | `1x3x512x512 -> 1x2x512x512` | 445.5 MB |       |        | Pruned                         |
| `DDColor_modelscope_512_quant8.mlpackage`             | `mlProgram` | iOS16+     | `1x3x512x512 -> 1x2x512x512` | 223.8 MB |       |        | INT8                           |
| `DDColor_modelscope_512_ios18.mlpackage`              | `mlProgram` | iOS18+     | `1x3x512x512 -> 1x2x512x512` | 445.5 MB |       |        | iOS 18 spec                    |
| `DDColor_modelscope_512_ios18_quant4.mlpackage`       | `mlProgram` | iOS18+     | `1x3x512x512 -> 1x2x512x512` | 112.7 MB |       |        | iOS18, 4-bit quant             |
| `DDColor_modelscope_512_ios18_pal3_kmeans.mlpackage`  | `mlProgram` | iOS18+     | `1x3x512x512 -> 1x2x512x512` | 84.4 MB  |       |        | iOS18, 3-bit palette (kmeans)  |
| `DDColor_modelscope_512_ios18_pal3_uniform.mlpackage` | `mlProgram` | iOS18+     | `1x3x512x512 -> 1x2x512x512` | 84.4 MB  |       |        | iOS18, 3-bit palette (uniform) |
| `DDColor_modelscope_512_pal1_kmeans.mlpackage`        | `mlProgram` | iOS16+     | `1x3x512x512 -> 1x2x512x512` | 28.9 MB  |       |        | 1-bit palette (kmeans)         |
| `DDColor_modelscope_512_pal1_uniform.mlpackage`       | `mlProgram` | iOS16+     | `1x3x512x512 -> 1x2x512x512` | 28.9 MB  |       |        | 1-bit palette (uniform)        |
| `DDColor_modelscope_512_pal2_kmeans.mlpackage`        | `mlProgram` | iOS16+     | `1x3x512x512 -> 1x2x512x512` | 56.7 MB  |       |        | 2-bit palette (kmeans)         |
| `DDColor_modelscope_512_pal2_uniform.mlpackage`       | `mlProgram` | iOS16+     | `1x3x512x512 -> 1x2x512x512` | 56.7 MB  |       |        | 2-bit palette (uniform)        |
| `DDColor_modelscope_512_pal4_kmeans.mlpackage`        | `mlProgram` | iOS16+     | `1x3x512x512 -> 1x2x512x512` | 112.2 MB |       |        | 4-bit palette (kmeans)         |
| `DDColor_modelscope_512_pal4_uniform.mlpackage`       | `mlProgram` | iOS16+     | `1x3x512x512 -> 1x2x512x512` | 112.2 MB |       |        | 4-bit palette (uniform)        |
| `DDColor_modelscope_512_pal6_kmeans.mlpackage`        | `mlProgram` | iOS16+     | `1x3x512x512 -> 1x2x512x512` | 167.8 MB |       |        | 6-bit palette (kmeans)         |
| `DDColor_modelscope_512_pal6_uniform.mlpackage`       | `mlProgram` | iOS16+     | `1x3x512x512 -> 1x2x512x512` | 167.8 MB |       |        | 6-bit palette (uniform)        |
| `DDColor_modelscope_512_pal8_kmeans.mlpackage`        | `mlProgram` | iOS16+     | `1x3x512x512 -> 1x2x512x512` | 223.4 MB |       |        | 8-bit palette (kmeans)         |
| `DDColor_modelscope_512_pal8_uniform.mlpackage`       | `mlProgram` | iOS16+     | `1x3x512x512 -> 1x2x512x512` | 223.4 MB |       |        | 8-bit palette (uniform)        |
| `DDColor_modelscope_512_pal_unique.mlpackage`         | `mlProgram` | iOS16+     | `1x3x512x512 -> 1x2x512x512` | 445.5 MB |       |        | Unique palette variant         |


---

## Image2Image (Anime2Sketch)

Anime/style artwork to sketch conversion. Original: [Mukosame/Anime2Sketch](https://github.com/Mukosame/Anime2Sketch) (MIT).

Models live in `Models-List/anime2sketch/`.

I/O contract summary:

- Main neural-network variants: `512x512 -> 512x512` (`spec4`, iOS13+)
- Ensemble overlay variants: pipeline `512x512 -> 1024x1024` (`spec7`, iOS16+)


| Model                                                         | Type            | Min target | I/O                    | Size     | Input | Output | Notes                             |
| ------------------------------------------------------------- | --------------- | ---------- | ---------------------- | -------- | ----- | ------ | --------------------------------- |
| `anime2sketch.mlpackage`                                      | `neuralNetwork` | iOS13+     | `512x512 -> 512x512`   | 207.6 MB |       |        | Base                              |
| `anime2sketch 2.mlpackage`                                    | `neuralNetwork` | iOS13+     | `512x512 -> 512x512`   | 207.6 MB |       |        | Alternate package name            |
| `anime2sketch_xcode.mlpackage`                                | `neuralNetwork` | iOS13+     | `512x512 -> 512x512`   | 207.6 MB |       |        | Xcode-optimized                   |
| `anime2sketch_xcode_fp16.mlpackage`                           | `neuralNetwork` | iOS13+     | `512x512 -> 512x512`   | 103.8 MB |       |        | FP16                              |
| `anime2sketch_xcode_quant8.mlpackage`                         | `neuralNetwork` | iOS13+     | `512x512 -> 512x512`   | 51.9 MB  |       |        | INT8                              |
| `anime2sketch_tmp_q8.mlpackage`                               | `neuralNetwork` | iOS13+     | `512x512 -> 512x512`   | 51.9 MB  |       |        | Temporary/experiment INT8 variant |
| `anime2sketch_xcode_archsame_quant4.mlpackage`                | `neuralNetwork` | iOS13+     | `512x512 -> 512x512`   | 26.0 MB  |       |        | Same arch, 4-bit                  |
| `anime2sketch_xcode_archsame_quant8.mlpackage`                | `neuralNetwork` | iOS13+     | `512x512 -> 512x512`   | 51.9 MB  |       |        | Same arch, 8-bit                  |
| `anime2sketch_xcode_archsame_pal4.mlpackage`                  | `neuralNetwork` | iOS13+     | `512x512 -> 512x512`   | 26.0 MB  |       |        | Same arch, pal4                   |
| `anime2sketch_xcode_lut4.mlpackage`                           | `neuralNetwork` | iOS13+     | `512x512 -> 512x512`   | 26.0 MB  |       |        | LUT 4-bit                         |
| `anime2sketch_xcode_lut6.mlpackage`                           | `neuralNetwork` | iOS13+     | `512x512 -> 512x512`   | 38.9 MB  |       |        | LUT 6-bit                         |
| `anime2sketch_xcode_linear4.mlpackage`                        | `neuralNetwork` | iOS13+     | `512x512 -> 512x512`   | 26.0 MB  |       |        | Linear 4-bit                      |
| `anime2sketch_xcode_hybrid_q4lut4_50.mlpackage`               | `neuralNetwork` | iOS13+     | `512x512 -> 512x512`   | 26.0 MB  |       |        | Hybrid quant                      |
| `anime2sketch_ensemble_overlay_esrgan_one_model.mlpackage`    | `pipeline`      | iOS16+     | `512x512 -> 1024x1024` | 86.7 MB  |       |        | Ensemble overlay + ESRGAN         |
| `anime2sketch_ensemble_overlay_esrgan_one_model_v2.mlpackage` | `pipeline`      | iOS16+     | `512x512 -> 1024x1024` | 86.7 MB  |       |        | Ensemble overlay + ESRGAN (v2)    |


---

## Thanks

Thanks to the authors of Real-ESRGAN, NAFNet, DDColor, and Anime2Sketch for the original models and code.

---

## Author

[Your Name]  
[Your Title / Role]  
Contact: [your@email.com](mailto:your@email.com)  
[GitHub](https://github.com/[your-username])
