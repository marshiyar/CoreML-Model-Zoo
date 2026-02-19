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


| Model                                         | I/O                              | Size    | Input | Output | Notes                    |
| --------------------------------------------- | -------------------------------- | ------- | ----- | ------ | ------------------------ |
| <code>RealESRGAN_<wbr>x2plus.<wbr>mlpackage</code>                 | `1x3x256x256 -> 1x3x512x512`     | 32.5 MB |       |        | Base 2x upscale          |
| <code>RealESRGAN_<wbr>x2plus_<wbr>flex.<wbr>mlpackage</code>            | `1x3x[64..1024]^2 -> dynamic 2x` | 32.5 MB |       |        | Flexible input size      |
| <code>RealESRGAN_<wbr>x2plus_<wbr>flex1280.<wbr>mlpackage</code>        | `1x3x[64..1280]^2 -> dynamic 2x` | 32.5 MB |       |        | Flex, max side 1280      |
| <code>RealESRGAN_<wbr>x2plus_<wbr>pruned.<wbr>mlpackage</code>          | `1x3x256x256 -> 1x3x512x512`     | 32.5 MB |       |        | Pruned                   |
| <code>RealESRGAN_<wbr>x2plus_<wbr>quant8.<wbr>mlpackage</code>          | `1x3x256x256 -> 1x3x512x512`     | 16.8 MB |       |        | INT8 quantized           |
| <code>RealESRGAN_<wbr>x2plus_<wbr>pal4.<wbr>mlpackage</code>            | `1x3x256x256 -> 1x3x512x512`     | 8.7 MB  |       |        | Palette 4-bit            |
| <code>RealESRGAN_<wbr>x2plus_<wbr>pal6.<wbr>mlpackage</code>            | `1x3x256x256 -> 1x3x512x512`     | 12.7 MB |       |        | Palette 6-bit            |
| <code>RealESRGAN_<wbr>x2plus_<wbr>pal8.<wbr>mlpackage</code>            | `1x3x256x256 -> 1x3x512x512`     | 16.9 MB |       |        | Palette 8-bit            |
| <code>RealESRGAN_<wbr>x2plus_<wbr>flex1280_<wbr>pruned.<wbr>mlpackage</code> | `1x3x[64..1280]^2 -> dynamic 2x` | 32.5 MB |       |        | Flex1280 + pruned        |
| <code>RealESRGAN_<wbr>x2plus_<wbr>flex1280_<wbr>quant8.<wbr>mlpackage</code> | `1x3x[64..1280]^2 -> dynamic 2x` | 16.8 MB |       |        | Flex1280 + INT8          |
| <code>RealESRGAN_<wbr>x2plus_<wbr>flex1280_<wbr>pal4.<wbr>mlpackage</code>   | `1x3x[64..1280]^2 -> dynamic 2x` | 8.7 MB  |       |        | Flex1280 + palette 4-bit |
| <code>RealESRGAN_<wbr>x2plus_<wbr>flex1280_<wbr>pal6.<wbr>mlpackage</code>   | `1x3x[64..1280]^2 -> dynamic 2x` | 12.7 MB |       |        | Flex1280 + palette 6-bit |
| <code>RealESRGAN_<wbr>x2plus_<wbr>flex1280_<wbr>pal8.<wbr>mlpackage</code>   | `1x3x[64..1280]^2 -> dynamic 2x` | 16.8 MB |       |        | Flex1280 + palette 8-bit |
| <code>RealESRGAN_<wbr>x2_<wbr>wrapped.<wbr>mlpackage</code>             | `1x3x256x256 -> 1x3x512x512`     | 32.5 MB |       |        | Wrapped pipeline variant |


### RealESRGAN x4

I/O contract summary:

- Models in this folder use `1x3x256x256 -> 1x3x1024x1024`
- Base package is `iOS15+` (`spec6`); compressed/slim variants are `iOS16+` (`spec7`)


| Model                                             | I/O                            | Size    | Input | Output | Notes                              |
| ------------------------------------------------- | ------------------------------ | ------- | ----- | ------ | ---------------------------------- |
| <code>RealESRGAN_<wbr>x4.<wbr>mlpackage</code>                         | `1x3x256x256 -> 1x3x1024x1024` | 32.5 MB | <img src="https://github.com/marshiyar/CoreML-Model-Zoo/blob/main/Models-List/RealESRGAN_x4/RealESRGAN_x4_model_outputs/input_images/RealESRGAN_x4_model_Input1.png?raw=true" width="120" /> | <img src="https://github.com/marshiyar/CoreML-Model-Zoo/blob/main/Models-List/RealESRGAN_x4/RealESRGAN_x4_model_outputs/output_images/output_images1/RealESRGAN_x4.png?raw=true" width="120" /> | Base 4x upscale                    |
| <code>RealESRGAN_<wbr>x4_<wbr>slim.<wbr>mlpackage</code>                    | `1x3x256x256 -> 1x3x1024x1024` | 16.8 MB |       | <img src="https://github.com/marshiyar/CoreML-Model-Zoo/blob/main/Models-List/RealESRGAN_x4/RealESRGAN_x4_model_outputs/output_images/output_images1/RealESRGAN_x4_slim.png?raw=true" width="120" /> | Slim architecture                  |
| <code>RealESRGAN_<wbr>x4_<wbr>slimmer.<wbr>mlpackage</code>                 | `1x3x256x256 -> 1x3x1024x1024` | 8.8 MB  |       | <img src="https://github.com/marshiyar/CoreML-Model-Zoo/blob/main/Models-List/RealESRGAN_x4/RealESRGAN_x4_model_outputs/output_images/output_images1/RealESRGAN_x4_slimmer.png?raw=true" width="120" /> | Slimmer architecture               |
| <code>RealESRGAN_<wbr>x4_<wbr>pruned.<wbr>mlpackage</code>                  | `1x3x256x256 -> 1x3x1024x1024` | 32.5 MB |       | <img src="https://github.com/marshiyar/CoreML-Model-Zoo/blob/main/Models-List/RealESRGAN_x4/RealESRGAN_x4_model_outputs/output_images/output_images1/RealESRGAN_x4_pruned.png?raw=true" width="120" /> | Pruned                             |
| <code>RealESRGAN_<wbr>x4_<wbr>quant8.<wbr>mlpackage</code>                  | `1x3x256x256 -> 1x3x1024x1024` | 16.8 MB |       | <img src="https://github.com/marshiyar/CoreML-Model-Zoo/blob/main/Models-List/RealESRGAN_x4/RealESRGAN_x4_model_outputs/output_images/output_images1/RealESRGAN_x4_quant8.png?raw=true" width="120" /> | INT8 quantized                     |
| <code>RealESRGAN_<wbr>x4_<wbr>pal4.<wbr>mlpackage</code>                    | `1x3x256x256 -> 1x3x1024x1024` | 8.8 MB  |       | <img src="https://github.com/marshiyar/CoreML-Model-Zoo/blob/main/Models-List/RealESRGAN_x4/RealESRGAN_x4_model_outputs/output_images/output_images1/RealESRGAN_x4_pal4.png?raw=true" width="120" /> | Palette 4-bit                      |
| <code>RealESRGAN_<wbr>x4_<wbr>arch_<wbr>b8_<wbr>nf48_<wbr>gc24_<wbr>xcode.<wbr>mlpackage</code> | `1x3x256x256 -> 1x3x1024x1024` | 6.6 MB  |       | <img src="https://github.com/marshiyar/CoreML-Model-Zoo/blob/main/Models-List/RealESRGAN_x4/RealESRGAN_x4_model_outputs/output_images/output_images1/RealESRGAN_x4_arch_b8_xcode.png?raw=true" width="120" /> | Architecture-slim (`b8,nf48,gc24`) |


---

## Image Denoising (NAFNet)

Image denoising with NAFNet (SIDD-trained, width 64). Original: [megvii-research/NAFNet](https://github.com/megvii-research/NAFNet).

Models live in `Models-List/NAFNet_SIDD_width64/`.

I/O contract summary:

- `1x3x512x512 -> 1x3x512x512`
- Type: `mlProgram`


| Variant                                                | I/O                          | Size     | Input | Output | Notes                          |
| ------------------------------------------------------ | ---------------------------- | -------- | ----- | ------ | ------------------------------ |
| <code>NAFNet_<wbr>SIDD_<wbr>width64_<wbr>512.<wbr>mlpackage</code>                    | `1x3x512x512 -> 1x3x512x512` | 221.7 MB |       |        | Base                           |
| <code>NAFNet_<wbr>SIDD_<wbr>width64_<wbr>512_<wbr>quant8.<wbr>mlpackage</code>             | `1x3x512x512 -> 1x3x512x512` | 111.8 MB |       |        | INT8                           |
| <code>NAFNet_<wbr>SIDD_<wbr>width64_<wbr>512_<wbr>ios18.<wbr>mlpackage</code>              | `1x3x512x512 -> 1x3x512x512` | 221.7 MB |       |        | iOS 18 spec                    |
| <code>NAFNet_<wbr>SIDD_<wbr>width64_<wbr>512_<wbr>ios18_<wbr>quant4.<wbr>mlpackage</code>       | `1x3x512x512 -> 1x3x512x512` | 56.7 MB  |       |        | iOS18, 4-bit quant             |
| <code>NAFNet_<wbr>SIDD_<wbr>width64_<wbr>512_<wbr>ios18_<wbr>pal3_<wbr>kmeans.<wbr>mlpackage</code>  | `1x3x512x512 -> 1x3x512x512` | 42.5 MB  |       |        | iOS18, 3-bit palette (kmeans)  |
| <code>NAFNet_<wbr>SIDD_<wbr>width64_<wbr>512_<wbr>ios18_<wbr>pal3_<wbr>uniform.<wbr>mlpackage</code> | `1x3x512x512 -> 1x3x512x512` | 42.5 MB  |       |        | iOS18, 3-bit palette (uniform) |
| <code>NAFNet_<wbr>SIDD_<wbr>width64_<wbr>512_<wbr>pal1_<wbr>kmeans.<wbr>mlpackage</code>        | `1x3x512x512 -> 1x3x512x512` | 14.9 MB  |       |        | 1-bit palette (kmeans)         |
| <code>NAFNet_<wbr>SIDD_<wbr>width64_<wbr>512_<wbr>pal1_<wbr>uniform.<wbr>mlpackage</code>       | `1x3x512x512 -> 1x3x512x512` | 14.9 MB  |       |        | 1-bit palette (uniform)        |
| <code>NAFNet_<wbr>SIDD_<wbr>width64_<wbr>512_<wbr>pal2_<wbr>kmeans.<wbr>mlpackage</code>        | `1x3x512x512 -> 1x3x512x512` | 28.7 MB  |       |        | 2-bit palette (kmeans)         |
| <code>NAFNet_<wbr>SIDD_<wbr>width64_<wbr>512_<wbr>pal2_<wbr>uniform.<wbr>mlpackage</code>       | `1x3x512x512 -> 1x3x512x512` | 28.7 MB  |       |        | 2-bit palette (uniform)        |
| <code>NAFNet_<wbr>SIDD_<wbr>width64_<wbr>512_<wbr>pal4_<wbr>kmeans.<wbr>mlpackage</code>        | `1x3x512x512 -> 1x3x512x512` | 56.3 MB  |       |        | 4-bit palette (kmeans)         |
| <code>NAFNet_<wbr>SIDD_<wbr>width64_<wbr>512_<wbr>pal4_<wbr>uniform.<wbr>mlpackage</code>       | `1x3x512x512 -> 1x3x512x512` | 56.3 MB  |       |        | 4-bit palette (uniform)        |
| <code>NAFNet_<wbr>SIDD_<wbr>width64_<wbr>512_<wbr>pal6_<wbr>kmeans.<wbr>mlpackage</code>        | `1x3x512x512 -> 1x3x512x512` | 83.9 MB  |       |        | 6-bit palette (kmeans)         |
| <code>NAFNet_<wbr>SIDD_<wbr>width64_<wbr>512_<wbr>pal6_<wbr>uniform.<wbr>mlpackage</code>       | `1x3x512x512 -> 1x3x512x512` | 83.9 MB  |       |        | 6-bit palette (uniform)        |
| <code>NAFNet_<wbr>SIDD_<wbr>width64_<wbr>512_<wbr>pal8_<wbr>kmeans.<wbr>mlpackage</code>        | `1x3x512x512 -> 1x3x512x512` | 111.6 MB |       |        | 8-bit palette (kmeans)         |
| <code>NAFNet_<wbr>SIDD_<wbr>width64_<wbr>512_<wbr>pal8_<wbr>uniform.<wbr>mlpackage</code>       | `1x3x512x512 -> 1x3x512x512` | 111.6 MB |       |        | 8-bit palette (uniform)        |


---

## Image Colorization (DDColor)

Grayscale image colorization. ModelScope variant. Original: [piddnad/DDColor](https://github.com/piddnad/DDColor).

Models live in `Models-List/DDColor/`.

I/O contract summary:

- `gray_rgb:1x3x512x512 -> ab:1x2x512x512`
- Type: `mlProgram`


| Variant                                               | I/O                          | Size     | Input | Output | Notes                          |
| ----------------------------------------------------- | ---------------------------- | -------- | ----- | ------ | ------------------------------ |
| <code>DDColor_<wbr>modelscope_<wbr>512.<wbr>mlpackage</code>                    | `1x3x512x512 -> 1x2x512x512` | 445.5 MB |       |        | Base                           |
| <code>DDColor_<wbr>modelscope_<wbr>512_<wbr>pruned.<wbr>mlpackage</code>             | `1x3x512x512 -> 1x2x512x512` | 445.5 MB |       |        | Pruned                         |
| <code>DDColor_<wbr>modelscope_<wbr>512_<wbr>quant8.<wbr>mlpackage</code>             | `1x3x512x512 -> 1x2x512x512` | 223.8 MB |       |        | INT8                           |
| <code>DDColor_<wbr>modelscope_<wbr>512_<wbr>ios18.<wbr>mlpackage</code>              | `1x3x512x512 -> 1x2x512x512` | 445.5 MB |       |        | iOS 18 spec                    |
| <code>DDColor_<wbr>modelscope_<wbr>512_<wbr>ios18_<wbr>quant4.<wbr>mlpackage</code>       | `1x3x512x512 -> 1x2x512x512` | 112.7 MB |       |        | iOS18, 4-bit quant             |
| <code>DDColor_<wbr>modelscope_<wbr>512_<wbr>ios18_<wbr>pal3_<wbr>kmeans.<wbr>mlpackage</code>  | `1x3x512x512 -> 1x2x512x512` | 84.4 MB  |       |        | iOS18, 3-bit palette (kmeans)  |
| <code>DDColor_<wbr>modelscope_<wbr>512_<wbr>ios18_<wbr>pal3_<wbr>uniform.<wbr>mlpackage</code> | `1x3x512x512 -> 1x2x512x512` | 84.4 MB  |       |        | iOS18, 3-bit palette (uniform) |
| <code>DDColor_<wbr>modelscope_<wbr>512_<wbr>pal1_<wbr>kmeans.<wbr>mlpackage</code>        | `1x3x512x512 -> 1x2x512x512` | 28.9 MB  |       |        | 1-bit palette (kmeans)         |
| <code>DDColor_<wbr>modelscope_<wbr>512_<wbr>pal1_<wbr>uniform.<wbr>mlpackage</code>       | `1x3x512x512 -> 1x2x512x512` | 28.9 MB  |       |        | 1-bit palette (uniform)        |
| <code>DDColor_<wbr>modelscope_<wbr>512_<wbr>pal2_<wbr>kmeans.<wbr>mlpackage</code>        | `1x3x512x512 -> 1x2x512x512` | 56.7 MB  |       |        | 2-bit palette (kmeans)         |
| <code>DDColor_<wbr>modelscope_<wbr>512_<wbr>pal2_<wbr>uniform.<wbr>mlpackage</code>       | `1x3x512x512 -> 1x2x512x512` | 56.7 MB  |       |        | 2-bit palette (uniform)        |
| <code>DDColor_<wbr>modelscope_<wbr>512_<wbr>pal4_<wbr>kmeans.<wbr>mlpackage</code>        | `1x3x512x512 -> 1x2x512x512` | 112.2 MB |       |        | 4-bit palette (kmeans)         |
| <code>DDColor_<wbr>modelscope_<wbr>512_<wbr>pal4_<wbr>uniform.<wbr>mlpackage</code>       | `1x3x512x512 -> 1x2x512x512` | 112.2 MB |       |        | 4-bit palette (uniform)        |
| <code>DDColor_<wbr>modelscope_<wbr>512_<wbr>pal6_<wbr>kmeans.<wbr>mlpackage</code>        | `1x3x512x512 -> 1x2x512x512` | 167.8 MB |       |        | 6-bit palette (kmeans)         |
| <code>DDColor_<wbr>modelscope_<wbr>512_<wbr>pal6_<wbr>uniform.<wbr>mlpackage</code>       | `1x3x512x512 -> 1x2x512x512` | 167.8 MB |       |        | 6-bit palette (uniform)        |
| <code>DDColor_<wbr>modelscope_<wbr>512_<wbr>pal8_<wbr>kmeans.<wbr>mlpackage</code>        | `1x3x512x512 -> 1x2x512x512` | 223.4 MB |       |        | 8-bit palette (kmeans)         |
| <code>DDColor_<wbr>modelscope_<wbr>512_<wbr>pal8_<wbr>uniform.<wbr>mlpackage</code>       | `1x3x512x512 -> 1x2x512x512` | 223.4 MB |       |        | 8-bit palette (uniform)        |
| <code>DDColor_<wbr>modelscope_<wbr>512_<wbr>pal_<wbr>unique.<wbr>mlpackage</code>         | `1x3x512x512 -> 1x2x512x512` | 445.5 MB |       |        | Unique palette variant         |


---

## Image2Image (Anime2Sketch)

Anime/style artwork to sketch conversion. Original: [Mukosame/Anime2Sketch](https://github.com/Mukosame/Anime2Sketch) (MIT).

Models live in `Models-List/anime2sketch/`.

I/O contract summary:

- Main neural-network variants: `512x512 -> 512x512` (`spec4`, iOS13+)
- Ensemble overlay variants: pipeline `512x512 -> 1024x1024` (`spec7`, iOS16+)


| Model                                                         | I/O                    | Size     | Input | Output | Notes                             |
| ------------------------------------------------------------- | ---------------------- | -------- | ----- | ------ | --------------------------------- |
| <code>anime2sketch.<wbr>mlpackage</code>                                      | `512x512 -> 512x512`   | 207.6 MB |       |        | Base                              |
| <code>anime2sketch 2.<wbr>mlpackage</code>                                    | `512x512 -> 512x512`   | 207.6 MB |       |        | Alternate package name            |
| <code>anime2sketch_<wbr>xcode.<wbr>mlpackage</code>                                | `512x512 -> 512x512`   | 207.6 MB |       |        | Xcode-optimized                   |
| <code>anime2sketch_<wbr>xcode_<wbr>fp16.<wbr>mlpackage</code>                           | `512x512 -> 512x512`   | 103.8 MB |       |        | FP16                              |
| <code>anime2sketch_<wbr>xcode_<wbr>quant8.<wbr>mlpackage</code>                         | `512x512 -> 512x512`   | 51.9 MB  |       |        | INT8                              |
| <code>anime2sketch_<wbr>tmp_<wbr>q8.<wbr>mlpackage</code>                               | `512x512 -> 512x512`   | 51.9 MB  |       |        | Temporary/experiment INT8 variant |
| <code>anime2sketch_<wbr>xcode_<wbr>archsame_<wbr>quant4.<wbr>mlpackage</code>                | `512x512 -> 512x512`   | 26.0 MB  |       |        | Same arch, 4-bit                  |
| <code>anime2sketch_<wbr>xcode_<wbr>archsame_<wbr>quant8.<wbr>mlpackage</code>                | `512x512 -> 512x512`   | 51.9 MB  |       |        | Same arch, 8-bit                  |
| <code>anime2sketch_<wbr>xcode_<wbr>archsame_<wbr>pal4.<wbr>mlpackage</code>                  | `512x512 -> 512x512`   | 26.0 MB  |       |        | Same arch, pal4                   |
| <code>anime2sketch_<wbr>xcode_<wbr>lut4.<wbr>mlpackage</code>                           | `512x512 -> 512x512`   | 26.0 MB  |       |        | LUT 4-bit                         |
| <code>anime2sketch_<wbr>xcode_<wbr>lut6.<wbr>mlpackage</code>                           | `512x512 -> 512x512`   | 38.9 MB  |       |        | LUT 6-bit                         |
| <code>anime2sketch_<wbr>xcode_<wbr>linear4.<wbr>mlpackage</code>                        | `512x512 -> 512x512`   | 26.0 MB  |       |        | Linear 4-bit                      |
| <code>anime2sketch_<wbr>xcode_<wbr>hybrid_<wbr>q4lut4_<wbr>50.<wbr>mlpackage</code>               | `512x512 -> 512x512`   | 26.0 MB  |       |        | Hybrid quant                      |
| <code>anime2sketch_<wbr>ensemble_<wbr>overlay_<wbr>esrgan_<wbr>one_<wbr>model.<wbr>mlpackage</code>    | `512x512 -> 1024x1024` | 86.7 MB  |       |        | Ensemble overlay + ESRGAN         |
| <code>anime2sketch_<wbr>ensemble_<wbr>overlay_<wbr>esrgan_<wbr>one_<wbr>model_<wbr>v2.<wbr>mlpackage</code> | `512x512 -> 1024x1024` | 86.7 MB  |       |        | Ensemble overlay + ESRGAN (v2)    |


---

## Thanks

Thanks to the authors of Real-ESRGAN, NAFNet, DDColor, and Anime2Sketch for the original models and code.

---

## Author

[Your Name]  
[Your Title / Role]  
Contact: [your@email.com](mailto:your@email.com)  
[GitHub](https://github.com/[your-username])
